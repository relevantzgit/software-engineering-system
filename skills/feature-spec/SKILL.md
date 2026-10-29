---
name: feature-spec
description: >-
  Author a rigorous, business-language feature specification from an idea or a
  discovered need — user-story based, with MoSCoW priorities, Given/When/Then
  acceptance criteria, scope seams, a permissions matrix, data/privacy flags, and
  tracked open questions. Use this whenever someone wants to write, draft,
  structure, refine, or review a feature spec, PRD, functional spec, requirements
  document, or user-story breakdown for a product feature — including loose asks
  like "spec this out", "turn this idea into requirements", "write up the stories
  for X", or "is this spec ready to build?". Produces a spec that reads for the
  business, not the build, and is ready to hand to a delivery team.
---

# Feature Spec

Draft a feature specification that describes **what users can do and see**, grounded
in agreed decisions, structured around user stories, and honest about what is still
open. The goal is a document a delivery team can pick up and build from — and that a
product owner can confidently sign off ("verify") because nothing load-bearing is
missing or unresolved.

## When to use this

Reach for this skill when turning a need into a governed feature spec, when filling out
a half-written one, or when reviewing whether a spec is ready to build. It works whether
you are writing from scratch or editing an existing document.

## The one idea that matters most

**Write for the business, not the build.** Describe the user-visible behaviour — what a
person can do, what they see, what the system decides on their behalf — not how it is
implemented. No endpoint contracts, schema changes, error codes, or test tables in the
spec body; a delivery team derives those from the spec when they pick it up. Name device
features (camera, push notifications, biometrics, location) in plain terms, never as SDKs
or permission APIs.

This matters because a spec written in implementation language ages badly, excludes the
non-engineers who need to agree to it, and quietly smuggles in design decisions nobody
ratified. Business language keeps the spec reviewable by the people who own the outcome.

## The template

Use the 14-section structure in [references/feature-spec-template.md](references/feature-spec-template.md).
Read it before writing, and copy it as the skeleton — do not invent your own section list,
because downstream readers rely on finding things where they expect them. If a section
does not apply, keep the heading and write `N/A — <reason>`; deleting it loses the signal
that it was considered.

## Workflow

### 1. Start with the user stories (§5) — they are the spine

Everything else in the spec references the user stories: screens realise them, business
rules constrain them, messages report on them, open questions block them. A story missed
here propagates as a gap everywhere. So write §5 first, before the prose around it.

Each story is **an outcome a user can observe**, phrased "As a &lt;persona&gt;, I can
&lt;do something&gt;, so that &lt;value&gt;." Give each one:
- A stable **ID** (`US-01`, `US-02`, …).
- A **priority**: Must / Should / Could / Won't (MoSCoW).
- At least **one happy-path and one "something goes wrong" acceptance criterion**, in
  **Given / When / Then** form. A story whose only criteria are happy-path is not
  specified — the failure behaviour is where real systems break and where builders
  otherwise guess.

### 2. Walk the full lifecycle before you freeze the story list

For the main thing the feature deals with, deliberately walk **create · view · change ·
cancel or close · restore**. Story lists built from a narrative reliably cover *create*
and *view* and silently drop the termination verbs — cancel, deactivate, revoke, expire,
supersede, delete. Walk the lifecycle for the primary entity and for every secondary
entity the stories touch. A missing stage needs either its own story, an explicit
out-of-scope entry, or an `N/A — reason`. A silent gap is the most common real defect.

### 3. Check the stories don't already belong to another spec

Before finalising scope, look at neighbouring specs for overlap. Where two specs touch the
same ground, record the seam in **§4 Out of scope of both**, each naming the other as the
owner. A boundary recorded in only one spec holds in neither — the other team won't know
to honour it.

### 4. Ground every claim in agreed decisions, not older drafts

Cite the **decision of record** for any rule, constraint, or permission — a decision log,
an agreed requirement, a signed-off policy. Prior spec versions, task tickets, and design
mockups drift; the agreed decision is the authority. Check whether a decision has been
superseded rather than trusting the first thing you find. Never invent a governing rule to
fill a gap — if the decision hasn't been made, that is an **Open Question** (§13), not an
assumption buried in a business rule.

For a **greenfield feature with no decision log, prior agreements, or neighbouring specs
yet**, say so plainly at the top of the spec, and treat each rule that would need a decision
as an Open Question. Expect such a spec to be open-question-heavy by design — that is honest
draft-stage work, not under-specification. A spec written inside an established governance
corpus should instead carry mostly citations and few open questions; the balance tells the
reader which situation they're in.

### 5. Check permissions against the authoritative access model (§11)

Fill §11 Who Can Do What from the project's agreed access/role model (an RBAC matrix or
equivalent) — do not re-derive who-can-do-what from scratch, because that is exactly where
quietly-wrong authorisation creeps in. Every persona in §11 should be a real role; every
action a story implies should have a matching permission; a permission the spec grants that
the access model withholds (or vice versa) is a defect, and visibility/tenancy mismatches
are the serious kind.

If no authoritative access model exists yet, fill §11 with your best proposal, mark the whole
table **provisional**, and log an Open Question to have it ratified — never present an
unratified permissions matrix as if it were confirmed.

### 6. Decide platform per story, and ask — never assume (§6.3)

If the feature ships on more than one platform (e.g. web and mobile), tag **every story,
screen, rule, and open question** with its platform: Web / Mobile / Both. **Ask the product
owner per story** which it is — offer a recommendation from the persona (e.g. end-customer
flows → Both; back-office configuration → Web) and let them confirm.

If no product owner is reachable (an unattended or batch run), do not stall and do not guess
silently: tag each story with the persona-based recommendation, mark those tags
**provisional**, and log one Open Question asking the PO to confirm the platform split.
"Never assume" means never *silently* assume — a recorded, owner-flagged assumption is the
correct fallback, and the same applies to any step above that would otherwise need a person
to answer. Then:
- Give every screen a design link **for each platform it is on**, or log an Open Question —
  never a placeholder link.
- Fill §6.3 so the per-platform build list agrees with the tags, note any behaviour
  differences (or "None"), and give every single-platform item a reason.
- For each device feature used, state its fallback when unavailable (no signal, permission
  refused), or "None".

If the feature is single-platform, say so once and move on — don't force the structure.

### 7. Flag personal or sensitive information (§8)

In §8 Information Captured, mark every field that is personal or sensitive. This is a
product and compliance decision, not a schema detail, and it is mandatory regardless of who
later designs the data model — downstream privacy obligations depend on it being flagged
here.

### 8. Write the spec and record what's unresolved honestly

Write the remaining sections in template order. Replace every `[placeholder]` and remove the
guidance lines. For anything genuinely undecided, add a row to **§13 Open Questions** with
an **owner**, the **stories it blocks**, and a due date if known.

**Never fabricate placeholder rows to disguise an unresolved item.** An invented screen,
rule, or design link reads as finished work and is worse than an honest open question,
because it hides the gap from everyone who trusts the document.

### 9. Finish and recommend a rigor pass before sign-off

A spec does not need to be complete to exist — a useful draft needs at least §1 and the §5
story list. The rest is required by the **§14 Definition of Ready** before it is verified,
not at every edit.

When the draft is ready, report:
- The spec is **a draft / unverified** — it is not committed to a delivery board yet.
- Recommend an **independent rigor review** (citation accuracy, completeness against §14,
  consistency of cross-cutting rules) **before** it is verified, because defects are cheap
  to fix while the spec is still a draft and expensive once work is committed against it.
- Verification (product-owner sign-off) is the gate that puts the feature into delivery —
  use §14 Ready as the checklist for it.

## Rules that keep a spec trustworthy

- **IDs are never reused.** When a story moves or is dropped, keep its ID and mark it
  `Moved to <feature>` or `Dropped — <reason>`. Reusing an ID silently breaks every
  reference to the old one.
- **No release, wave, or phase markings in the spec body** ("Phase 2", "MVP", "mobile
  later"). Phasing belongs on the work-tracker items, not the spec — it rots the spec the
  moment the plan changes. Express deferred scope as an out-of-scope entry naming the owner,
  or a single-platform item with a reason. (Feature flags are fine — they are not release
  markings.)
- **The spec is authoritative for user-facing wording.** Where a mockup's text differs from
  §9 Messages & Errors, the spec wins and the difference is raised as a design change
  request.
- **Every section applies or says why not.** Use `N/A — reason`; never silently delete a
  section or collapse a required table into prose.
- **No open question may block a Must story at verification.** A Must story resting on an
  unresolved question is not ready — resolve it or lower the priority.
- **Report what is solid as clearly as what is missing.** A review that only lists problems
  misrepresents the state of the spec.

## Optional: tool-backed authoring

This skill is tool-agnostic and works fully in plain Markdown. If your organisation already
runs a requirements/governance system exposed over MCP, **and you ask Claude to use it**, the
skill can read your decision log or access model from that system (steps 4 and 5) and register
the spec through it (step 9) instead of working from memory. Only the source of truth and the
destination change; the methodology above is identical.

The skill never reaches for such a system on its own — you configure it separately and invoke
it explicitly. It is not bundled with, started by, or required by this skill.
