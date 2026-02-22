# How We Work

```
INTERNAL NOTE: This page is the full process documentation. The homepage has a five-step
summary; this page is the version for founders who want to understand exactly what they are
committing to. Write it as if a founder is reading it at 11pm before deciding whether to
submit the waitlist intake form. It should be the most operational page on the site.
Anchor links #zero-to-one and #one-to-hundred are referenced by other pages and must remain
exactly as written here.
```

---

[Home](index.md) | [Services](services.md) | [Case Studies](case-studies/index.md) | [Blog](blogs/index.md) | [About](about.md) | [Developer Store](developer-store.md) | [Join the Waitlist](waitlist.md)

---

Most agencies keep their process vague because a vague process is easier to not be held to.
Valnee publishes this page because a founder who understands exactly what they are buying
is a better client and, frankly, a better partner. If any part of what is described here
does not fit how you need to work, that is important information — and the time to discover
it is before the engagement starts, not after.

The process below is organized into two tracks: the 0 to 1 track for new builds, and the
1 to 100 track for existing codebases. Both tracks follow the same five-step structure, but
the specific work and the outputs at each step are different. A note on what is common to
both tracks: scope is always defined in writing before work begins, code always lives in the
client's repository from day one, and documentation is always produced throughout the
engagement rather than compressed into the final days.

---

## The 0 to 1 Process: Building From Scratch {#zero-to-one}

```
INTERNAL NOTE: This section covers the full process for founders who have no existing
codebase. The five steps below are the same steps summarized on the homepage, expanded
with specific detail about timing, responsibilities, and outputs.
```

This track is for founders who have a validated product concept and need a first working
version built. You do not need to be technical to participate fully in this process. The
work of translating product thinking into technical decisions is Valnee's responsibility,
not yours. Your responsibility is to know what the product needs to do and to be available
for structured review at the end of each delivery cycle.

### Step 1: Intake and Scoping

**Who does what:** Valnee schedules a structured 45-minute call and arrives with a pre-prepared
brief template. Before the call, the client is asked to fill in what they know: the problem
being solved, the target users, the core workflows the product needs to support, any existing
work product (wireframes, competitive analysis, user research), and constraints on timeline
or budget.

**What happens on the call:** The call is a structured conversation, not a pitch. Valnee
asks specific questions to understand what is known, what is assumed, and what is unknown.
The goal is to produce a scope document after the call, and the quality of that document
depends on the quality of the information gathered.

**What is produced:** A written scope document delivered within five business days of the
call. The document specifies the features included in the first version, the features
explicitly excluded, the technical stack and the reasons for each choice, the delivery
timeline with milestones, the payment schedule, the communication format, and the definition
of done. The client reviews the scope document and approves it in writing before any work
begins. Changes to scope after approval are handled through a written change process.

**Typical duration:** One to two weeks from initial contact to approved scope document.

---

### Step 2: Technology Selection and Architecture

**Who does what:** Valnee makes the technology decisions. For non-technical founders, this
means Valnee selects the programming language, the framework, the database, the hosting
infrastructure, the authentication approach, and the third-party services the product will
integrate with. Each decision is documented with the alternatives considered and the
reasoning for the choice.

**What is produced:** An architecture decision record — a written document the client
receives and owns. For non-technical founders, the document includes a plain-language
summary of each decision alongside the technical detail. The goal is not to require you
to understand every technical choice, but to ensure that the record exists so that any
future developer can understand why the system was built the way it was.

The repository is created in the client's version control account during this step. All
subsequent code is committed there. There is no moment at the end of the engagement when
the codebase "transfers" — it belongs to the client throughout.

**Typical duration:** Three to five business days.

---

### Step 3: Delivery in Defined Cycles

**Who does what:** Valnee builds in two-week delivery cycles. At the start of each cycle,
a cycle plan is shared with the client specifying exactly what will be built during that
cycle. At the end of each cycle, the client is given access to a deployed, working increment
of the product — not a status report, not a presentation, but something they can interact
with.

**Client review process:** After each cycle, the client has three business days to review
the delivered increment and submit feedback. Feedback is reviewed at the start of the next
cycle. Significant feedback that changes what will be built in the next cycle is handled
through the scope change process — a written change request with time and cost implications
noted before the change is accepted. Minor feedback — usability adjustments, label changes,
workflow tweaks within the agreed scope — is incorporated without a formal change process.

**What is produced:** Working, deployed software at the end of each cycle. Cumulative
documentation in the project wiki, updated after each cycle. A cycle summary note
describing what was built, any decisions made during the cycle, and what comes next.

**Typical duration:** Two weeks per cycle. Most MVP builds run four to six cycles.

---

### Step 4: Documentation and Handoff Preparation

**Who does what:** Documentation is written continuously throughout the engagement. The
handoff preparation step is a final review and completion pass that happens in the last
cycle. Valnee reviews all existing documentation for completeness, records a walkthrough
video of the delivered system, and prepares the deployment runbook.

**What is produced:** The handoff package includes:

- Internal architecture documentation describing how the system is structured and how the
  main components interact
- A data model reference describing the key entities, their relationships, and the reasoning
  behind the design decisions
- API documentation for any endpoints exposed by the system
- A deployment runbook with step-by-step instructions for deploying the application,
  rolling back a deployment, and responding to the most common operational issues
- Environment configuration documentation listing all required environment variables and
  where to obtain their values
- A recorded video walkthrough of the delivered system (typically 20 to 40 minutes)

The standard applied to the handoff package: a competent developer who has never seen the
codebase should be able to understand the system, deploy it, and add a new feature using
only the documentation provided. If the documentation does not meet this standard, it is
a delivery deficiency, not a developer's problem to solve independently.

**Typical duration:** The final cycle, running concurrently with the last round of feature
delivery.

---

### Step 5: Post-Delivery Review

**Who does what:** Two weeks after the final delivery, Valnee schedules a structured review
call. By this point, the client's team has had time to work with the delivered system, and
questions or issues that were not apparent during development often become visible in
production use.

**What happens on the call:** The call covers three areas. First, any functionality
questions — things that behave differently than expected or that the documentation does not
adequately explain. Second, operational questions — deployment issues, environment
configuration questions, monitoring concerns. Third, a brief retrospective on the engagement
itself — what worked well in the process and what could have been better.

**What is produced:** A final sign-off document confirming that the deliverables meet the
agreed scope. Any items identified on the call that are genuine delivery deficiencies — not
new scope requests, but things that should have been delivered and were not — are addressed
before the sign-off document is issued.

**Typical duration:** One hour call, plus any follow-up work identified. Total post-delivery
window is typically one to two weeks.

---

## The 1 to 100 Process: Improving What Exists {#one-to-hundred}

```
INTERNAL NOTE: This section covers the full process for founders who have an existing
codebase. The five steps below parallel the 0-to-1 track but are adapted for the specific
challenges of working with existing systems. The audit step is the most important difference.
Address the emotional concern: Valnee has seen all kinds of codebases and will not be
judgmental about what it finds.
```

This track is for founders who have a product in production and need it improved — whether
that means fixing systemic reliability problems, improving performance, making the codebase
more maintainable, or preparing the system for a significant increase in load. You will
have code that was written under time pressure, possibly by multiple contractors, possibly
through a mix of intentional decisions and shortcuts. This is not unusual. The starting
point of every 1 to 100 engagement is an honest assessment of what exists, not a judgment
about how it was built.

### Step 1: Intake and Codebase Access

**Who does what:** Valnee schedules a structured intake call with the same format as the
0 to 1 track. The additional requirement for existing codebases is access to the codebase
itself before the scoping document is finalized. Valnee cannot scope codebase work
accurately without seeing the codebase. This access is granted through read-only repository
access — no production credentials, no access to live user data.

**What happens on the call:** The intake conversation for a 1 to 100 engagement focuses
on the symptoms: what is failing, what is slow, what is hard to change, what has been
tried, and what the cost of the problem is in terms of development time, user impact, or
operational risk. The most useful preparation for this call is a list of the three to five
specific problems you most need solved, ranked by impact on your ability to build and grow.

**What is produced:** An intake summary note and a preliminary scope direction. The full
scope document follows the audit step, because the audit is what makes accurate scoping
possible for existing codebase work.

**Typical duration:** One to two weeks from initial contact to codebase access granted.

---

### Step 2: Codebase Audit and Assessment

**Who does what:** Valnee conducts a structured audit of the codebase. The audit covers
the architecture, the test coverage, the deployment process, the dependency management
approach, and the specific areas that were flagged as problems in the intake conversation.
The audit is not a casual code review — it is a systematic examination using a defined
checklist that Valnee has developed across multiple similar engagements.

**What the audit looks for:** Areas of high complexity with low test coverage — these are
the places where changes are most likely to introduce new problems. External dependencies
that are outdated, incorrectly used, or undocumented. Deployment processes that are manual,
fragile, or poorly understood. Data model decisions that are causing query performance
problems or making new features harder to build. Security issues in the areas most commonly
exploited: authentication, authorization, data exposure, and input handling.

**What is produced:** A written audit report organized by severity and impact. Each finding
includes a description of the problem, the evidence for it, the risk it creates, and a
recommended approach to addressing it. The report is prioritized: the items at the top of
the list are those that will produce the most improvement in development speed and system
stability when addressed. The report belongs to the client regardless of whether a
subsequent improvement engagement proceeds.

**Typical duration:** One to two weeks depending on the size of the codebase.

---

### Step 3: Scoping and Prioritization

**Who does what:** After the audit, Valnee and the client review the findings together and
agree on the scope of the improvement engagement. Not every finding in the audit report
needs to be addressed immediately — some are important to know about but do not need to
be fixed in the current engagement. The scoping conversation is about determining which
improvements will produce the most value for the client's current situation.

**What is produced:** A scope document specifying which improvements will be made, in what
order, using what approach, on what timeline, and at what cost. The scope document for a
codebase improvement engagement is typically more detailed than for a new build, because
the nature of working with existing code requires acknowledging that some findings may be
more complex than they appear from the audit and that the scope may need to be adjusted if
unexpected complexity is encountered. That process is documented: if the complexity of a
specific improvement is significantly different from what was estimated, Valnee notifies the
client in writing with a revised estimate before proceeding.

**Typical duration:** Three to five business days from audit report delivery to approved
scope.

---

### Step 4: Delivery in Defined Cycles

**Who does what:** Improvement work proceeds in two-week cycles with the same review
structure as the 0 to 1 track. The difference is that the nature of the work is often
less visible to a non-technical reviewer — fixing an architecture problem or improving
a database query may not change what the product looks like but does change how it behaves
under load or how fast new features can be added.

For this reason, each cycle in a codebase improvement engagement ends with a written cycle
summary that describes what was changed, what tests were added or modified, what
measurements were taken, and what the observable impact is on the problem that was
targeted. Where the impact is measurable — response time, error rate, deployment duration —
the measurement is included in the summary.

**Concurrent development policy:** Improvement work can proceed alongside the client team's
ongoing feature development as long as the client's team is communicating about active
changes in the areas Valnee is working on. The intake checklist for codebase engagements
includes setting up a simple communication protocol for exactly this purpose.

**Typical duration:** Two weeks per cycle. Most codebase improvement engagements run two
to five cycles.

---

### Step 5: Documentation Update and Post-Delivery Review

**Who does what:** At the end of a codebase improvement engagement, the existing
documentation is updated to reflect the current state of the system. If the system had
no documentation before the engagement, a baseline documentation set is created: architecture
overview, deployment runbook, and a description of the most complex or most frequently
changed areas of the codebase.

**What is produced:** Updated or new architecture documentation, updated or new deployment
runbook, and a final findings document summarizing what was changed from the state
described in the audit report, what was not changed and why, and what the client should
watch over the next three to six months as the improved system operates in production.

The post-delivery review call follows the same format as the 0 to 1 track — a structured
two-week-after call to address any questions that arose after the client team had time to
work with the improved system.

**Typical duration:** One to two weeks including the post-delivery review call.

---

## Communication Throughout an Engagement

Valnee uses asynchronous-first communication. This means most project communication happens
in writing, on a schedule, rather than through ad hoc calls. This is not a cost-cutting
measure — it is a quality measure. Written communication creates a record, allows for
more careful formulation of questions and answers, and does not require both parties to
be available at the same moment.

**Weekly written update:** Every Monday, Valnee sends a written project update to the
primary client contact. The update covers what was completed in the previous week, what is
planned for the current week, any decisions or input needed from the client, and any risks
or issues that have arisen.

**Response time commitment:** Valnee responds to client questions within one business day
during active engagements. If a question requires more than a quick response, Valnee will
acknowledge receipt within one business day and provide a more complete response within
three.

**Scheduled calls:** In addition to the cycle review calls, clients can request a
30-minute discussion call at any point during an engagement with 48 hours notice. Calls
are used for decisions or discussions that genuinely benefit from a synchronous format —
not for status updates, which are handled in writing.

**Scope changes in writing:** Any change to the agreed scope — including additions, removals,
and modifications to existing scope — is handled through a written change request. The
change request includes what is being changed, why, the time implication, and the cost
implication. The client approves or declines in writing before any work related to the
change begins.

---

## What Happens When Things Go Wrong

Software projects encounter unexpected complexity. Estimated timelines are based on the
best available information at the time of scoping and will occasionally be wrong. Valnee's
commitment is not that surprises will never happen — it is that when they do, the client
finds out immediately, in writing, with a clear explanation of what changed and what the
options are.

When a technical discovery changes the estimated timeline or cost of a specific piece of
scope, Valnee communicates it as soon as the discovery is made — not at the end of the
cycle, not when the delay is unavoidable, but at the point of discovery. The communication
includes the nature of the discovery, the revised estimate, and the available options:
proceed at the revised scope and cost, modify the scope to stay within the original budget,
or defer the affected work to a future engagement. The client makes the decision; Valnee
provides the information needed to make it.

What Valnee will not do is absorb scope expansion silently and present a surprise invoice
at the end of the engagement. What Valnee will also not do is discover a problem and
continue without telling the client in the hope that it resolves itself. The commitment is
to transparency about the real state of the project, regardless of whether that transparency
is comfortable to deliver.

---

[Ready to start? Join the waitlist.](waitlist.md)

---

**Navigation:** [Home](index.md) | [Services](services.md) | [Case Studies](case-studies/index.md) | [Blog](blogs/index.md) | [About](about.md) | [Developer Store](developer-store.md) | [Join the Waitlist](waitlist.md)

**Contact:** hello@valnee.com

&copy; Valnee Solutions. All rights reserved.
