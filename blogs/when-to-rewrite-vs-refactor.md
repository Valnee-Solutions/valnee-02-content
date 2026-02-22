# When to Refactor Your Codebase and When to Rewrite It

```
INTERNAL NOTE: Target audience: 1-to-100 founders who have a product in production with
a codebase that is causing problems. Tone: analytical, even-handed. This is a real debate
in engineering and the post should treat it seriously — presenting both cases honestly
rather than advocating strongly for one position. Closes with a diagnostic framework and
links to services.md and waitlist.md for founders who want an assessment.
```

---

[Blog](index.md) | [Home](../index.md) | [Services](../services.md) | [Process](../process.md) | [Join the Waitlist](../waitlist.md)

---

**Tag:** [1-to-100] | **Read time:** Approximately 14 minutes | **Published:** January 2026

---

At some point in the life of almost every company that has been building software for more
than two years, the question surfaces: should we rewrite the codebase or fix what we have?
It is one of the most consequential technical decisions a company makes, and it is made
badly more often than it is made well. Badly in both directions — teams that rewrite when
they should have refactored, and teams that keep refactoring when a rewrite was genuinely
the better path. Both errors are costly. Both are avoidable with a clearer framework for
making the decision.

This post presents the honest case for each option and a set of diagnostic questions that
help determine which one applies to your situation. It does not arrive at a clean universal
answer — the right answer depends on the specific codebase, the specific team, and the
specific constraints — but it should give you a clearer basis for the decision than "our
developers are frustrated" or "we heard a rewrite is always a mistake."

---

## The Case for Refactoring

Refactoring — the process of improving the internal structure of a codebase without changing
its observable behavior — is the right choice in most situations where a codebase is
causing problems. The case for refactoring rests on a few durable observations about how
software and organizations work in practice.

**The existing codebase contains institutional knowledge you cannot fully recover in a
rewrite.**
Every line of code in a production system encodes a decision someone made at some point.
Most of those decisions are not documented — they are expressed in the code itself. Some
of those decisions were wrong; many of them were correct responses to constraints or
requirements that are no longer visible in the documentation (because the documentation
does not exist or because the requirement changed). When you rewrite a system, you discard
not only the bad decisions but also the accumulated good decisions, the edge case handling,
the subtle behavior that your users depend on without explicitly asking for it. The rewrite
team will rediscover many of these decisions the hard way — by missing them and watching
the new system fail in ways the old system did not.

**Refactoring can be done incrementally, which means it can be done while the business
continues operating.**
A rewrite almost always requires a period of parallel operation — the old system and the
new system running simultaneously, with a cutover at some defined point. That parallel
period is expensive and operationally complex. Incremental refactoring — improving one
area of the codebase at a time, behind tests, with a defined rollback plan — does not
require the same level of operational disruption. The business does not stop while the
codebase is being improved.

**Most of the problems in a struggling codebase are concentrated, not distributed.**
A common mental model of a "bad codebase" is one where every part is equally problematic.
In practice, codebase problems tend to be clustered. There are usually two to four areas
of the codebase that account for the majority of the maintenance burden, the bug rate, and
the development friction. Identifying those areas specifically and addressing them through
refactoring often produces 80 percent of the benefit of a full rewrite at 20 percent of
the cost and risk.

**The team that writes the second system is not immune to the same pressures that
compromised the first.**
The rewrite will be built under time pressure. It will be scoped optimistically. It will
encounter requirements that were not anticipated. It will accumulate technical debt as
deadlines approach. The conditions that led to the problems in the current codebase do
not disappear because the team starts fresh — they reassert themselves during the new
build, often producing a second system with a different set of problems but a similar
overall quality level.

---

## The Case for Rewriting

There are genuine situations where refactoring is not the right answer and a rewrite is.
These situations are less common than the frustration that typically drives rewrite
conversations, but they are real.

**The architecture has a fundamental structural problem that cannot be addressed
incrementally.**
Some architectural decisions are load-bearing in a way that prevents incremental change.
If the core data model is wrong — if it makes the queries that the product needs inherently
slow, or if it makes the business logic inherently complex, or if it creates a structural
impedance between what the product needs to do and how the data is organized — refactoring
around that constraint produces diminishing returns. Each incremental improvement makes
the local area better while the global constraint remains. In these situations, a focused
rewrite of the affected core component — not necessarily the entire system, but the specific
part that is structurally wrong — is the practical path.

**The technology is genuinely obsolete in a way that creates operational risk.**
The word "obsolete" is used loosely in engineering conversations, often meaning "unfashionable"
rather than "unsupported." The relevant threshold for a rewrite decision is not fashionable
versus unfashionable — it is supported versus unsupported in a way that creates security
or operational risk. If a product is running on a runtime version or a framework version
that no longer receives security updates, and if the upgrade path to a supported version
is not practical due to breaking changes, a rewrite of the affected component may be the
lower-risk option compared to continued operation on an unsupported dependency.

**The team that built the system is completely unavailable and the codebase is
undocumented.**
A codebase is useful in proportion to its comprehensibility. A codebase that was built by
a team that is no longer available, that has no documentation, and that reflects idiosyncratic
choices that require the original author's knowledge to understand, may cost more to bring
to a maintainable state through archaeology and reverse engineering than a targeted rewrite
of the most problematic components. This is not a justification for rewriting because the
code is messy — mess can be cleaned up. It is a justification for rewriting when the effort
to understand what exists is comparable to the effort to rebuild it correctly.

**The scope of what the product needs to do has changed fundamentally.**
Sometimes a product grows to the point where what it needs to do is qualitatively different
from what it was built to do. A system that was built to manage fifty users per organization
and now needs to manage fifty thousand is not necessarily in this category — that is a
scaling problem, typically addressable through targeted performance work. A system that was
built as a single-tenant application and needs to become multi-tenant typically is in this
category — because multi-tenancy, done correctly, affects the data model, the authentication
and authorization layer, the deployment model, and the billing infrastructure in ways that
are difficult to retrofit incrementally without effectively rewriting those components anyway.

---

## A Diagnostic Framework

The following questions are intended to help determine which option — refactoring or
rewriting — is more appropriate for a specific situation. They are not a scoring system.
They are prompts for a structured conversation about the specific codebase and the
specific constraints.

**1. Can you identify the specific areas of the codebase that are causing the most problems?**
If yes: you have the information needed to scope a refactoring engagement. The problems
are specific and addressable. A rewrite would address them, but so would targeted
refactoring at lower cost and risk.
If no: the problem is not well-understood enough to scope either option correctly. The
first step is an audit, not a decision.

**2. Is the core data model preventing the product from doing things it needs to do?**
If yes: this is the strongest indicator that a rewrite of the data layer — not necessarily
the entire system — may be warranted. Data model problems are genuinely hard to refactor
around.
If no: the problems are likely in the application logic, the integration layer, or the
deployment infrastructure — areas that are typically refactorable.

**3. Is the system currently deployable by someone other than the person who built it?**
If yes: the codebase has a deployable baseline, which makes incremental improvement
practical.
If no: the first priority is establishing that baseline. That is a prerequisite for both
refactoring and rewriting, because the new system will also need to be deployable.

**4. How much of the current system's behavior do you fully understand?**
If most: you have the context to write a new version that captures what the current system
does correctly while fixing what it does incorrectly.
If little: a rewrite will rediscover the missing context in production. This is expensive.
The answer here is to understand the system before rewriting it — which is most of the
work of refactoring it.

**5. Does the product have a test suite that covers the core behavior?**
If yes: refactoring is significantly safer. Tests provide the signal that a refactoring
change has not altered observable behavior.
If no: adding tests to the current system is a prerequisite for effective refactoring —
and it is also something that would be valuable in a rewrite, which means the work of
adding tests is valuable regardless of which path is taken.

**6. Is the team that would do the rewrite the same team that built the current system?**
If no, and the current system has no documentation: the rewrite team is starting from a
lower baseline than it appears. Budget additional time and cost for requirements archaeology
before the new system will be reliably equivalent to the old one.
If yes: the team carries the institutional knowledge that a rewrite needs to succeed. This
is the best scenario for a rewrite if the other conditions warrant it.

**7. What is the consequence of a six-month period of reduced development velocity?**
Both a well-managed refactoring engagement and a well-managed rewrite will reduce the
team's capacity for new feature development during the improvement period. A rewrite
typically reduces it more, for longer. If the business cannot afford that constraint —
if competitor pressure, customer commitments, or runway make a reduction in development
velocity dangerous — that is a strong argument for incremental refactoring over a full
rewrite.

---

## What We Have Seen in Practice

Across codebase engagements, the honest observation is this: founders who advocate for a
rewrite usually have a genuine problem, but the problem is rarely what they think it is.
The experience of a frustrating codebase — slow development, mysterious bugs, fragile
deployments — feels global. It feels like everything is wrong. The audit almost always
reveals that the problem is concentrated in two or three specific areas, and that those
areas are addressable through targeted work that does not require rebuilding the rest of
the system.

The cases where a rewrite was genuinely the right recommendation have involved specific,
structural problems: a data model that created irresolvable query performance issues,
a single-tenant architecture that a mid-size enterprise customer required to be multi-tenant,
a system running on a runtime that was three major versions out of support with no viable
upgrade path. In each of these cases, the recommendation was not "rewrite everything" —
it was "rewrite this specific component, and here is why incrementally refactoring it would
cost more than rebuilding it."

The rewrite instinct is understandable. Starting fresh feels like it should be faster and
cleaner than untangling existing complexity. In practice, the complexity that created the
problems in the first system tends to resurface in the second system unless the root causes
are understood and explicitly addressed. Understanding those root causes is most of the
work of a good refactoring engagement. If you do that work, you often find that the
refactoring path is shorter than the rewrite path, not longer.

---

## The Honest Closing Position

Most codebases can be refactored. Most rewrite instincts, examined carefully, turn out to
be refactoring opportunities in disguise. The cases that genuinely warrant a rewrite exist,
but they are specific and they can be identified through a structured audit before the
decision is made.

If you are dealing with a codebase that is slowing your team down and are uncertain which
path is right, the right first step is to understand what you have before committing to
either option. A structured audit produces that understanding. It also produces a document
you own, regardless of what you decide to do next.

[See the Codebase Rescue service for how Valnee approaches this work.](../services.md#codebase-rescue)

For an example of a refactoring engagement in practice, the
[Project Pluto case study](../case-studies/project-pluto.md) documents a situation where
a rewrite was considered and targeted refactoring was chosen — and what the outcome was.

[Back to blog](index.md) | [Start a conversation about your codebase](../waitlist.md)

---

**Navigation:** [Home](../index.md) | [Services](../services.md) | [Process](../process.md) | [Case Studies](../case-studies/index.md) | [About](../about.md) | [Developer Store](../developer-store.md) | [Join the Waitlist](../waitlist.md)

**Contact:** hello@valnee.com

&copy; Valnee Solutions. All rights reserved.
