# Feature Specification Template

Copy this structure as the skeleton of a new feature spec. Keep the section order and the
headings — downstream readers rely on finding things where they expect them. If a section
does not apply, keep the heading and write `N/A — <reason>`.

Replace every `[placeholder]`, fill the tables, and delete the 📝 guidance lines before the
spec is considered a draft worth sharing.

**Provisional content:** where a section is required but you could not confirm its content
(no decision of record, no ratified access model, no product-owner answer yet), fill it with
your best proposal, prefix the row or cell with **⚠ provisional**, and back it with an Open
Question in §13. A provisional entry is honest; a confident-looking but unratified one is not.

---

# [Feature name]

| | |
|---|---|
| **Status** | Draft / Unverified |
| **Owner** | [product owner] |
| **Platforms** | [Web / Mobile / Both / single] |
| **Last updated** | [date] |

## 1. Feature Summary
📝 Two or three sentences: what this feature is and the outcome it delivers. No implementation.

## 2. Feature Story
- **Problem today** — [what is hard or missing now]
- **What changes** — [the new capability, in business terms]
- **Success measures** — [how we will know it worked]

## 3. Personas
📝 Who uses this. One row per persona.

| Persona | Description | Main platform |
|---|---|---|
| [name] | [what they do] | [Web / Mobile / Both] |

## 4. Scope

**In scope**
- [capability]

**Out of scope**
📝 Name the owning feature for anything deliberately handed elsewhere — a seam must appear in both specs.

| Item | Covered by / reason |
|---|---|
| [item] | [owning feature, or reason] |

## 5. User Stories & Acceptance Criteria
📝 The spine of the spec. Walk the full lifecycle: create · view · change · cancel/close · restore.
Group under subheadings if there are more than ten.
📝 Use **Won't** for work this feature deliberately will not do at all. For work handed to
another feature or deferred, use the §4 Out of scope table naming the owner — not a phase or
"later" label (see the no-phase-markings rule).

### US-01 — [As a <persona>, I can <do something>, so that <value>]
- **Priority:** Must / Should / Could / Won't
- **Platform:** Web / Mobile / Both

| AC | Type | Given | When | Then | Platform |
|---|---|---|---|---|---|
| AC-01 | Happy path | [context] | [action] | [outcome] | Both |
| AC-02 | Something goes wrong | [context] | [action] | [outcome] | Both |

## 6. User Journey & Screens

### 6.1 Journey
📝 The end-to-end path through the feature, step by step, in business terms.

### 6.2 Screens
| Screen | Stories | Web design | Mobile design | Design status |
|---|---|---|---|---|
| [name] | US-01 | [link or §13] | [link or §13] | [Ready / Pending] |

### 6.3 Web & Mobile Delivery
📝 Omit this section for a single-platform feature (note it once in §1 instead).

- **What gets built, per platform** — Web: [stories/screens]; Mobile: [stories/screens] (must agree with the §5/§6.2 tags)
- **Differences** — [behaviour that differs by platform, or *None*]
- **Single-platform items** — [item · platform · reason · Revisit? Y/N]
- **Device features used** — [feature · fallback when unavailable, or *None*]

## 7. Business Rules
| ID | Rule | Applies to (stories) | Platform | Source decision |
|---|---|---|---|---|
| BR-01 | [constraint or invariant, in business terms] | US-01 | Both | [decision ref] |

## 8. Information Captured
📝 Flag personal/sensitive fields — this is a compliance decision, mandatory regardless of schema design.

| Field | Description | Personal or sensitive? |
|---|---|---|
| [field] | [what it is] | Yes / No |

## 9. Messages & Errors
| ID | Trigger (story) | Message the user sees | Where (web) | Where (mobile) |
|---|---|---|---|---|
| MSG-01 | US-01 | [user-facing wording] | [placement] | [placement] |

## 10. Notifications
| ID | Trigger | Channel | What it says | On tap / fallback |
|---|---|---|---|---|
| NT-01 | [event] | [email / push / in-app] | [content] | [push: what it opens; fallback if off] |

## 11. Who Can Do What
📝 Fill from the authoritative access/role model. Do not re-derive permissions from scratch.

| Action | [Role A] | [Role B] | [Role C] |
|---|---|---|---|
| [action] | Yes | Own only | No |

## 12. Dependencies & Assumptions
- **Depends on** — [other features, systems, data]
- **Assumptions** — [what we are taking as given]

## 13. Open Questions
📝 Every unresolved item lives here with an owner. No open question may block a Must story at verification.

| # | Question | Owner | Blocks | Due |
|---|---|---|---|---|
| Q1 | [the decision at stake] | [owner] | US-01 | [date] |

## 14. Definition of Ready & Done

**Ready for build** (checked before verification)
- [ ] Every story has acceptance criteria, including a "something goes wrong" case
- [ ] Every screen has a design link, or is logged as an open question
- [ ] Business rules, messages, and notifications are written out (or `N/A — reason`)
- [ ] Who-can-do-what is confirmed against the access model
- [ ] Personal/sensitive information is flagged in §8
- [ ] No open question blocks a Must story
- [ ] Platform tagging and §6.3 complete (multi-platform features)
- [ ] Reviewed with [stakeholders]

**Done** (checked at build exit — not a readiness criterion)
- [ ] Behaviour matches every acceptance criterion
- [ ] User-facing wording matches §9
- [ ] Personal information is only visible to the right people
