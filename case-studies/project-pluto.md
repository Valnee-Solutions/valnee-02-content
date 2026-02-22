# Case Study: Project Pluto

```
INTERNAL NOTE: This is the full case study for the logistics SaaS engagement (internally
called Project Pluto). It follows the standard case study structure: client context,
the problem, what Valnee found in the audit, what was built, results with numbers,
a client quote, and generalizable lessons. Written for the 1-to-100 audience — founders
with existing codebases experiencing systemic reliability problems.
```

---

[Case Studies](index.md) | [Home](../index.md) | [Services](../services.md) | [Process](../process.md) | [Join the Waitlist](../waitlist.md)

---

**Service used:** [Codebase Rescue and Refactoring](../services.md#codebase-rescue)

**Client type:** Logistics SaaS, Series A stage

**Engagement duration:** 11 weeks (2-week audit + 9-week improvement engagement)

---

## Client Context

The client is a B2B SaaS company serving freight brokers and small logistics operators.
Their platform manages the full lifecycle of a shipping order: intake from the customer,
matching to a carrier, tracking updates, and payment settlement. At the time of the
engagement, the company had approximately 2,200 active business accounts, was processing
between 800 and 1,400 orders per day, and had a twelve-person team including four engineers.

The platform had been built over roughly two years, primarily by a two-person engineering
team that had scaled to four. The codebase was Rails on the backend with a React front end.
The infrastructure ran on a major cloud provider with a standard relational database. None
of this was unusual for a company at that stage — the architecture was sensible for the
early period of the company, and the four engineers were competent.

The problem was not that the codebase was poorly built. The problem was that it had not
evolved to match the demands now being placed on it, and the specific area under most
pressure — the order processing pipeline — had accumulated complexity that the current
team did not fully understand.

---

## The Problem

Order processing failures had been part of the platform's operational reality for as long
as the engineering team could remember. Early on, the failure rate was low enough to manage
manually: a support team member would notice a failed order, escalate to engineering, and
the order would be reprocessed within a few hours. Customers experienced the occasional
delay, but the volume was low enough that it did not significantly affect the business.

By the time the engagement started, the situation had changed. The company had grown to a
volume where the 6 percent failure rate — orders that failed to process correctly and
required manual intervention — represented between 50 and 85 failed orders per day. The
support team was spending a significant portion of their capacity on manual order recovery.
Carriers were flagging the company as a reliability concern. Two enterprise account prospects
had specifically asked about order processing reliability during sales conversations, and the
honest answer had complicated those deals.

The engineering team had spent time trying to address the problem. They had fixed specific
bugs as they surfaced, added retry logic in several places, and improved logging. The failure
rate had not meaningfully improved. Their hypothesis was that the problem was related to
a specific external carrier API that behaved inconsistently. Valnee's audit found that this
hypothesis was partially correct but incomplete.

---

## What Valnee Found in the Audit

The audit began with read-only access to the repository and the production log archives
for the previous 90 days. The first step was a quantitative analysis of the failure logs —
not reading code, but understanding the patterns. Which orders failed? When did they fail?
What did they have in common? What preceded the failure in the logs?

The analysis produced three findings that the engineering team had not clearly identified:

**Finding one: Race conditions in concurrent order state transitions.**
The order processing pipeline allowed multiple processes to operate on the same order
simultaneously under certain conditions. When two processes attempted to transition an
order's state at the same moment — which happened when a carrier update and a customer
update arrived within milliseconds of each other — the pipeline did not handle the
concurrency correctly. The result was an order that ended up in an inconsistent state,
neither completed nor explicitly failed, that the system did not know how to recover
automatically. The engineering team had attributed many of these failures to the carrier
API hypothesis because the carrier update was one of the two concurrent events. The carrier
API was not the root cause — the lack of proper concurrency handling was.

**Finding two: Silent error swallowing in the carrier integration layer.**
The integration with the inconsistent carrier API the engineering team had identified was
indeed problematic, but not in the way they had diagnosed. The carrier API did return
errors — but those errors were being swallowed by a broad exception handler that logged
a generic error message and returned a success response to the calling code. The calling
code, receiving a success response, proceeded as if the carrier update had been applied.
The order would then reach a later stage of the pipeline where the expected carrier
update was not present, causing the failure at that later stage in a way that obscured
the original cause. The fix the engineering team had applied — retry logic — was being
applied at the wrong stage, after the error had already been obscured.

**Finding three: Missing idempotency on payment settlement.**
The payment settlement step — the step where the platform charges the customer and
pays the carrier — had no idempotency guarantees. If the settlement process was interrupted
and retried, it could attempt to execute the same payment twice. The platform had partial
protections against this in the database layer, but they were not applied consistently
across all payment paths. This finding was not the largest contributor to the failure rate
in the current data, but it was the highest-risk finding in the audit: a double-charge
incident at scale would be a serious operational and reputational problem.

---

## What Valnee Built

The improvement engagement was scoped to address all three findings, in order of severity
and implementation complexity. The constraint agreed on during scoping was that the front
end and the surrounding application logic would not be touched — only the order processing
pipeline and the integrations directly connected to it. This was a deliberate choice to
minimize the risk of the improvement work introducing new problems in unrelated areas of
the application.

**Concurrency handling — weeks 1 through 4:**
The order processing pipeline was refactored to use optimistic locking for state transitions.
Each order carries a version number. A state transition only succeeds if the process
attempting the transition is operating on the same version of the order that is currently
in the database. A concurrent attempt to transition the same order fails explicitly and
is retried with the current version. This is a standard pattern for this problem in Rails,
but implementing it correctly in the existing pipeline required significant restructuring
of the state machine logic. The refactored pipeline was deployed behind a feature flag
and tested against 10 percent of production traffic before full rollout.

**Carrier integration error handling — weeks 3 through 6:**
The broad exception handler in the carrier integration was replaced with explicit handling
for each error category the carrier API returned. Network errors, rate limit responses,
carrier-side processing errors, and data validation errors are now handled specifically,
with each error type having a defined outcome: immediate retry, delayed retry, escalation
to a human queue, or explicit failure with a customer-facing notification. The integration
now surfaces errors at the point where they occur rather than propagating them silently
to later pipeline stages. The inconsistent carrier API that the engineering team had
identified turned out to have a specific set of conditions under which it returned malformed
responses — those conditions are now detected and handled without cascading into pipeline
failures.

**Payment idempotency — weeks 7 through 9:**
Idempotency keys were added to all payment operations across all payment paths. The
implementation used the payment processor's native idempotency support where available
and a database-level idempotency table for the cases where the payment processor did not
provide it. Every payment operation, regardless of how it is triggered, now checks the
idempotency record before executing. Duplicate attempts are detected and rejected before
reaching the payment processor. This change also included a reconciliation pass over the
previous three months of payment records to identify any historical duplicate charges
that had not been caught by the partial protections previously in place. One historical
duplicate was found, which the client resolved directly with the affected customer.

---

## Results

Order processing reliability reached 99.7 percent within six weeks of the fully deployed
pipeline changes. The remaining 0.3 percent of failures are cases where carriers are
unreachable for extended periods — an external constraint that Valnee's changes did not
eliminate but did isolate: these failures now appear in a dedicated queue and generate
immediate notifications rather than surfacing as generic processing errors.

Manual order recovery by the support team dropped from approximately 60 cases per day
at the peak to an average of 4 to 6 per day, all of which are genuine carrier-related
incidents rather than platform-induced failures. The support team lead reported that the
order recovery workload that had been consuming 30 percent of the team's capacity was
effectively eliminated.

Deployment time for the order processing pipeline specifically dropped from a manual,
engineer-supervised 90-minute process to an automated 8-minute deployment. This was a
side effect of the testing infrastructure added during the improvement engagement — the
pipeline now has a comprehensive test suite that runs on every deployment and serves as
a checkpoint that the previous process required a human to substitute for.

Two of the enterprise account prospects that had raised concerns about reliability signed
contracts within three months of the platform improvements. The client's sales team
attributed the reliability improvements directly to their ability to answer reliability
questions with specific data in subsequent conversations.

---

## What the Client Said

"We had been living with the order failure problem for so long that it had become part of
how we operated. We had a support workflow, a recovery process, we had absorbed the cost
into our margins. What Valnee showed us in the audit was that the problem was not
fundamental to our architecture — it was three specific, fixable things. The engagement
took eleven weeks. The support workload from order failures essentially disappeared. I
wish we had done this two years earlier."

— Engineering Lead, Project Pluto

---

## Lessons for Similar Situations

These observations are drawn from this engagement and are applicable to founders in
comparable situations.

**The engineering team's hypothesis was not wrong — it was incomplete.**
The carrier API hypothesis was based on real observation: there was a correlation between
carrier API interactions and order failures. The audit did not invalidate that observation —
it traced the correlation to its actual root cause. This is the value of an audit-first
approach: it does not assume that existing diagnosis is wrong, it traces existing observations
to their underlying causes.

**Broad exception handlers are an underappreciated source of reliability problems.**
The pattern of catching a broad exception, logging a generic message, and returning
a success response is common in codebases that were built under time pressure. It is also
one of the most difficult problems to diagnose from production logs, because the failure
appears to happen somewhere other than where it actually happened. Any codebase audit
should include a specific pass looking for this pattern.

**Incremental improvement deployed behind feature flags is lower-risk than full-cycle
replacement.**
Every change in this engagement was deployed in stages, with the ability to roll back to
the previous state immediately if problems appeared. This meant the improvement work itself
did not introduce new production incidents. For any codebase change that touches a business-
critical flow, this approach is worth the additional deployment complexity.

---

[Is your situation similar? Tell us about your project.](../waitlist.md)

[Back to case studies](index.md)

---

**Navigation:** [Home](../index.md) | [Services](../services.md) | [Process](../process.md) | [Case Studies](index.md) | [Blog](../blogs/index.md) | [About](../about.md) | [Join the Waitlist](../waitlist.md)

**Contact:** hello@valnee.com

&copy; Valnee Solutions. All rights reserved.
