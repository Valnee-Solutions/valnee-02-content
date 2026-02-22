# How We Work

[Home](index.md) | [Services](services.md) | [Case Studies](case-studies/index.md) | [Blog](blogs/index.md) | [About](about.md) | [Developer Store](developer-store.md) | [Get Started](waitlist.md)

---

Most agencies keep their process vague because a vague process is harder to be held to. We publish this page because a founder who understands exactly what they're buying is a better partner — and the time to find a mismatch is before work begins, not after.

The process runs on two tracks: **0 to 1** for new builds, and **1 to 100** for existing codebases. Both tracks follow the same five-step structure. What's common to both: scope is always defined in writing before work begins, code always lives in your repository from day one, and documentation is always produced throughout the engagement.

---

## The 0 to 1 Process: Building From Scratch {#zero-to-one}

For founders who have a validated product concept and need a first working version built. You don't need to be technical. Translating product thinking into technical decisions is Valnee's job. Your job is to know what the product needs to do and to be available for structured review at the end of each delivery cycle.

```
IMAGE SUGGESTION: A simple horizontal timeline showing the five steps — Intake, Architecture, Build Cycles, Handoff, Review. Clean and minimal, no icons needed.
```

### Step 1: Intake and Scoping

A structured 45-minute call. Before the call, we ask you to fill in what you know: the problem, the target users, the core workflows, any existing wireframes or research, and your timeline and budget constraints.

The output is a written scope document delivered within five business days. It specifies what's included, what's explicitly excluded, the technology stack, the delivery timeline, the payment schedule, the communication format, and the definition of done. No work begins until you approve it in writing.

*Typical duration: 1–2 weeks from first contact to approved scope.*

---

### Step 2: Technology Selection and Architecture

We make the technology decisions. Stack, database, hosting, authentication, third-party integrations — each decision is documented with the alternatives considered and the reasoning behind the choice.

The output is an architecture decision record you own. For non-technical founders, it includes a plain-language summary alongside the technical detail. The repository is created in your version control account during this step. All subsequent code is committed there.

*Typical duration: 3–5 business days.*

---

### Step 3: Delivery in Defined Cycles

Work proceeds in two-week delivery cycles. At the start of each cycle, a plan is shared specifying exactly what will be built. At the end of each cycle, you get access to a deployed, working increment — not a status report, something you can actually interact with.

After each cycle, you have three business days to review and submit feedback. Minor adjustments are incorporated without a formal process. Significant changes that alter scope are handled through a written change request with time and cost implications noted before acceptance.

*Typical duration: 2 weeks per cycle. Most MVP builds run 4–6 cycles.*

---

### Step 4: Documentation and Handoff

Documentation is written throughout the engagement. The handoff package includes:

- Architecture documentation describing how the system is structured
- A data model reference
- API documentation for any exposed endpoints
- A deployment runbook with step-by-step instructions
- Environment configuration documentation
- A recorded video walkthrough of the delivered system (typically 20–40 minutes)

The standard: a competent developer who's never seen the codebase should be able to understand it, deploy it, and add a feature using only the documentation provided.

*Typical duration: Runs concurrently with the final delivery cycle.*

---

### Step 5: Post-Delivery Review

Two weeks after final delivery, we schedule a structured review call. By this point, questions and issues that weren't visible during development often appear in real use.

The call covers functionality questions, operational issues, and a brief retrospective on the engagement. The output is a final sign-off document confirming the deliverables meet the agreed scope. Any genuine delivery deficiencies — not new scope requests, but things that should have been included and weren't — are addressed before sign-off.

*Typical duration: 1-hour call, plus any follow-up. Total post-delivery window: 1–2 weeks.*

---

## The 1 to 100 Process: Improving What Exists {#one-to-hundred}

For founders who have a product in production and need it improved. The code may have been written under time pressure, by multiple contractors, or through a mix of deliberate decisions and shortcuts. That's not unusual. The starting point of every 1 to 100 engagement is an honest assessment of what exists — not a judgment about how it was built.

### Step 1: Intake and Codebase Access

Same structured intake call as the 0 to 1 track, with one addition: we need read-only access to the codebase before the scope document is finalized. Scoping codebase work without seeing the codebase produces inaccurate estimates.

The intake conversation focuses on symptoms: what's failing, what's slow, what's hard to change, what's been tried, and what the cost of the problem is in terms of development speed, user impact, or operational risk.

*Typical duration: 1–2 weeks from first contact to codebase access granted.*

---

### Step 2: Codebase Audit and Assessment

A structured audit covering the architecture, test coverage, deployment process, dependency management, and the specific problem areas identified in the intake call. The audit is systematic, not a casual review.

The output is a written audit report organized by severity and impact. Each finding includes a description of the problem, the evidence for it, the risk it creates, and a recommended approach. The report is prioritized: items at the top will produce the most improvement in development speed and system stability when addressed. This report belongs to you regardless of whether a subsequent improvement engagement proceeds.

*Typical duration: 1–2 weeks depending on codebase size.*

---

### Step 3: Scoping and Prioritization

After the audit, we review findings together and agree on the improvement scope. Not every finding needs to be addressed immediately — some are important to know about but don't need to be fixed in this engagement. The conversation is about which improvements will produce the most value for your current situation.

The output is a scope document specifying which improvements will be made, in what order, on what timeline, and at what cost.

*Typical duration: 3–5 business days from audit delivery to approved scope.*

---

### Step 4: Delivery in Defined Cycles

Improvement work proceeds in two-week cycles with the same review structure as the 0 to 1 track. Because much of this work happens below the surface — architecture changes, query optimizations, deployment improvements — each cycle ends with a written summary describing what was changed, what tests were added, what was measured, and what the observable impact is on the targeted problem. Where impact is measurable (response time, error rate, deployment duration), the numbers are included.

*Typical duration: 2 weeks per cycle. Most codebase improvement engagements run 2–5 cycles.*

---

### Step 5: Documentation Update and Post-Delivery Review

At the end of the engagement, existing documentation is updated to reflect the current state of the system. If no documentation existed, a baseline set is created: architecture overview, deployment runbook, and a description of the most frequently changed areas of the codebase.

The output also includes a final findings document summarizing what changed from the audit state, what wasn't changed and why, and what to watch over the next several months as the improved system operates in production.

The post-delivery review call follows the same format as the 0 to 1 track.

*Typical duration: 1–2 weeks including the post-delivery review.*

---

## Communication

Valnee uses async-first communication. Most project communication happens in writing on a schedule, not through ad hoc calls. Written communication creates a record and allows for more careful formulation of questions and answers.

**Weekly written update:** Every Monday, a written update covering what was completed, what's planned, any decisions needed from you, and any risks or issues that have arisen.

**Response time:** Questions are acknowledged within one business day during active engagements. If a full response needs more time, you'll get an acknowledgment within one business day and a complete response within three.

**Calls:** Available for decisions that genuinely benefit from a synchronous format. Request with 48 hours notice. Not used for status updates — those are handled in writing.

**Scope changes:** Always in writing. Every change includes what's being changed, why, the time implication, and the cost implication. No work on a change begins until you approve it in writing.

---

## When Things Go Wrong

Software projects encounter unexpected complexity. Estimated timelines are based on the best available information at the time of scoping and will occasionally be wrong. Our commitment is not that surprises will never happen — it's that when they do, you find out immediately, in writing, with a clear explanation and a set of options.

When a technical discovery changes the timeline or cost of a specific piece of scope, we communicate it at the point of discovery — not at the end of the cycle. The communication includes the nature of the discovery, the revised estimate, and the options: proceed at the revised scope and cost, modify scope to stay within the original budget, or defer the affected work. You make the decision; we provide the information needed to make it.

---

[Ready to start? Submit a project brief.](waitlist.md)

---

**Navigation:** [Home](index.md) | [Services](services.md) | [Case Studies](case-studies/index.md) | [Blog](blogs/index.md) | [About](about.md) | [Developer Store](developer-store.md) | [Get Started](waitlist.md)

**Contact:** hello@valnee.com

**Legal:** [Privacy Policy](privacy-policy.md) | [Refund Policy](refund-policy.md)

&copy; Valnee Solutions. All rights reserved.
