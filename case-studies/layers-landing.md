# Case Study: Layers Landing Page

```
INTERNAL NOTE: This is the full case study for the non-technical founder MVP engagement
(Layers Landing Page). It follows the same standard case study structure as project-pluto.md.
Written for the 0-to-1 audience — non-technical founders who need to understand what
working with Valnee looks like from the first conversation through launch.
```

---

[Case Studies](index.md) | [Home](../index.md) | [Services](../services.md) | [Process](../process.md#zero-to-one) | [Join the Waitlist](../waitlist.md)

---

**Service used:** [MVP Development](../services.md#mvp-development)

**Client type:** Solo founder, B2B productivity SaaS, pre-seed stage

**Engagement duration:** 13 weeks (2-week scoping + 11-week build)

---

## Client Context

The founder — we will call her N.A., with her consent — had spent twelve years in operations
and product management roles at mid-size B2B software companies. She had a specific and
well-defined frustration with how teams managed layered approval workflows: the tools that
existed were either too heavyweight for small teams or too generic to handle the specific
branching logic that approval workflows required. She had validated the problem with
twenty-two interviews across her professional network, all of whom described the same
friction she had identified. Several had expressed interest in paying for a solution.

N.A. had no technical background. She had used no-code tools for personal projects but
had correctly assessed that a no-code approach would not give her the workflow flexibility
her product concept required. She had spoken to two freelance developers before contacting
Valnee — one had quoted a price well above her budget without a detailed scope, and one
had started work without a formal scope, delivered two weeks of code she could not review
or understand, and then become unavailable. She arrived at Valnee with a clear product
concept, a validated market, a six-month runway, 340 people on a waitlist, and a significant
amount of anxiety about the development process.

---

## The Problem She Brought to Valnee

N.A.'s primary need was a working product — deployed, usable, and in the hands of her
waitlist subscribers — within her runway window. That was the constraint that mattered most.
Secondary to that, she needed to understand what she was building well enough to talk about
it credibly with early users and potential investors. Her previous experience with freelancers
had left her feeling like a passenger in the development of her own product. She wanted
to be an informed participant, not just a client waiting for updates.

The specific product she was building — call it Layers — was a B2B web application that
allowed teams to define multi-step approval workflows with conditional branching. A request
enters the workflow, moves through a defined set of approvers in sequence or in parallel
depending on conditions, and generates a record of the full approval history. The product
needed user authentication with team-based access control, a workflow builder with a visual
representation of the approval chain, an approval inbox for each user showing their pending
actions, and a subscription billing integration with tiered plans.

None of this was unusually complex by SaaS standards. The challenge was doing it within
eleven weeks at a standard that a technically literate investor or a mid-size company's IT
team would find credible.

---

## How Valnee Approached the Engagement

### Weeks 1 and 2: Scoping and Technology Selection

The first week was the intake conversation and a product clarification session. The intake
conversation followed Valnee's standard format. The product clarification session was
specific to the nature of N.A.'s product: approval workflows have complex state — a request
can be in many possible states depending on how many approvers it has, what each approver
has done, and what conditions were set in the workflow definition. Before writing any code,
Valnee needed to understand exactly what the product needed to handle and exactly what it
did not need to handle in version one.

The output of the scoping step was a scope document that specified, feature by feature,
what the MVP would do and — equally important — what it would not do. Several capabilities
that N.A. had assumed would be in version one were deferred to version two: custom email
notifications, audit log export, and workflow versioning. These deferrals were not arbitrary.
Each one was deferred because it would add complexity without being necessary for the core
use case the twenty-two validation interviewees had described. N.A. reviewed and approved
the scope document. The deferred items were documented in a future-scope list, not discarded.

Technology selection produced a straightforward stack: Next.js for the front end and the
API layer, PostgreSQL for the database, a major authentication provider for user and team
management, and a major payment processor for subscription billing. Each choice was
documented with the alternatives considered. For N.A., the summary was: these tools are
well-documented, widely used for exactly this kind of product, and will be familiar to
any developer she hires after the engagement.

### Weeks 3 through 13: Build

The build proceeded in five two-week delivery cycles with one additional cycle for hardening
and handoff preparation.

**Cycle 1: Core data model, authentication, and team management.**
The first cycle built the foundational layer: the database schema, the authentication
integration, and the ability for a user to create an account, invite team members, and
manage their team's settings. At the end of cycle 1, N.A. could create an account,
invite a colleague, and see both accounts in a basic team settings screen. The
authentication and team management layer was the least visible to end users but the
most critical to get right before building everything that depended on it.

**Cycle 2: Workflow definition and builder.**
The workflow builder was the core of the product — the interface where a user defines
the approvers, the order, and the conditions for their approval chain. This cycle built
the data model for workflow definitions and a functional (not polished) interface for
creating and editing them. At the end of cycle 2, N.A. could create a workflow with
multiple approvers, define conditional branching, and save the workflow definition.

**Cycle 3: Request submission and approval inbox.**
This cycle built the user-facing workflow execution: the ability to submit a request
through a defined workflow and for each approver to see their pending approvals and
act on them. By the end of cycle 3, the core product loop — define a workflow, submit a
request, approve it — was working end to end for the first time. N.A. walked through it
with a former colleague from her validation interviews. The feedback from that session
shaped three specific adjustments in cycle 4.

**Cycle 4: Billing integration and plan management.**
Subscription billing was implemented using the chosen payment processor's standard
SaaS billing pattern: free trial, two paid plans, credit card collection, and automatic
renewal. Team plan and individual plan pricing was implemented as defined in the scope
document. This cycle also incorporated the three adjustments from the cycle 3 user test.

**Cycle 5: Polish, testing, and performance baseline.**
The final development cycle was not for new features — it was for the quality of what
had been built. Error states that had been left as rough were improved. The workflow
builder interface received the visual polish deferred from cycle 2. A test suite was
written covering the approval state machine, the billing integration, and the authentication
flows. A performance baseline was established: median page load times, API response times,
and database query durations were measured and documented. Nothing in the performance
baseline was alarming; having the baseline documented means any future degradation is
detectable.

**Cycle 6: Documentation and handoff.**
The final cycle produced the handoff package: architecture documentation, data model
reference, deployment runbook, API documentation for the internal endpoints, and a
40-minute recorded walkthrough of the codebase. The repository had been in N.A.'s
account from the first commit. The documentation made it a codebase she could hand to
any competent developer and have them understand it.

---

## Results

The product launched to N.A.'s waitlist on a Tuesday, eleven weeks after scoping was
approved. She had 340 subscribers on the waitlist. Sixty converted to free trials in the
first week. Fourteen converted to a paid plan within thirty days of launch.

Three months after launch, N.A. closed a pre-seed round. The investors she spoke to cited
the product's technical credibility — specifically that it was built on a standard stack,
had a clean codebase, and had documentation — as a factor in their confidence. One investor
noted that most pre-seed SaaS products they reviewed were built on no-code tools or had
codebases that would require significant work before a technical team could extend them.
Layers had neither of those problems.

N.A. made her first engineering hire six months after launch, using the architecture
documentation and the codebase walkthrough as the primary onboarding materials. The hire
reported that the documentation was the clearest they had seen in an early-stage product.

The product has since grown to over 800 active teams. N.A. and her engineering team continue
to operate the codebase that the engagement delivered, with significant extensions built on
top of the original architecture. None of the foundational architecture decisions have
required replacement.

---

## What the Founder Said

"I had already had one bad experience with a freelancer before I found Valnee. The difference
was immediate. The first thing Valnee did was write down exactly what we were building and
what we were not building. I had never had that from a developer before. Every week, I saw
working software. I understood what was being built and why. When the product launched, I
felt like I genuinely understood what I had built. That confidence mattered when I was
talking to investors — I was not performing confidence, I actually had it."

— N.A., Founder, Layers

---

## Lessons for Similar Situations

These observations are drawn from this engagement and are applicable to founders in
comparable situations.

**Scope reduction in the first version is almost always the right call.**
Three features that N.A. initially assumed were required for version one were deferred to
version two. None of the sixty early users in the first month asked for any of them. All
three have since been built, in the order of actual user demand, rather than the order
of initial assumptions. The scope document and the deferred features list made this
possible: nothing was lost, and the version one build was not slowed by features that
users did not need immediately.

**Documentation written during the build is fundamentally different from documentation
written after.**
The handoff package for this engagement was produced as part of the build, not as a
final-week task. Every architecture decision was documented when it was made. The
deployment runbook was written when the deployment process was set up. The data model
reference was updated whenever the schema changed. This is a discipline issue, not a
resourcing issue — documentation produced in parallel with the build reflects the actual
state of the system at each point. Documentation written at the end reflects the author's
memory of the system, which is a different and less reliable thing.

**A clean architecture decision record has direct value in early-stage fundraising.**
Investors at the pre-seed stage do not typically conduct deep technical due diligence,
but they do form impressions of technical quality based on whether the founding team can
answer questions about their technical choices with specificity. The architecture decision
record produced in this engagement gave N.A. specific, justified answers to every
technical question she received. This was not spin — the answers were accurate because
the decisions had been made carefully and documented honestly.

---

[Ready to build your product? Start with a scoping call.](../waitlist.md)

[Back to case studies](index.md)

---

**Navigation:** [Home](../index.md) | [Services](../services.md) | [Process](../process.md) | [Case Studies](index.md) | [Blog](../blogs/index.md) | [About](../about.md) | [Join the Waitlist](../waitlist.md)

**Contact:** hello@valnee.com

&copy; Valnee Solutions. All rights reserved.
