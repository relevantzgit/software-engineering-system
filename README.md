# feature-spec-authoring

A Claude Code plugin that packages one skill — **feature-spec** — for authoring rigorous,
business-language feature specifications.

## What it does

When you ask Claude to write, draft, structure, or review a feature spec (or a PRD,
functional spec, requirements doc, or user-story breakdown), the `feature-spec` skill guides
it to produce a specification that:

- reads **for the business, not the build** (no endpoints, schemas, or error codes in the body);
- is built around **user stories** with MoSCoW priorities and Given/When/Then acceptance criteria;
- walks the **full lifecycle** (create · view · change · cancel/close · restore) so termination cases aren't missed;
- records **scope seams** with neighbouring features, a **permissions matrix**, and **personal/sensitive-data flags**;
- tracks everything unresolved as **Open Questions** with owners — never fabricated placeholders;
- ends with a **Definition of Ready** checklist for sign-off.

A copy-ready 14-section template ships in
[`skills/feature-spec/references/feature-spec-template.md`](skills/feature-spec/references/feature-spec-template.md).

## Intended purpose

This skill is a **methodology and template for writing feature specifications**. It operates
entirely on text the user provides and produces a Markdown document. It does not connect to
any remote service, collect any data, or require any account.

## Example prompts

These demonstrate the core functionality. Each produces a complete or partial feature spec.

1. **From an idea:** "Spec out a self-service password reset feature for our web and mobile
   banking app. Users request a reset from the login screen, get a one-time code, and set a
   new password."
2. **From a one-liner:** "Turn this into a proper feature spec with user stories and
   acceptance criteria: let account admins invite teammates by email and assign them a role."
3. **Review an existing draft:** "Here's a draft spec for our document-sharing feature — check
   whether it's ready to build and tell me what's missing." *(attach or paste the draft)*
4. **Fill a gap:** "I have the user stories for our refund flow but no acceptance criteria or
   open questions — flesh those out."

## Contents

```
plugin/
├── .claude-plugin/
│   └── plugin.json
├── README.md
├── SECURITY.md
├── LICENSE
└── skills/
    └── feature-spec/
        ├── SKILL.md
        └── references/
            └── feature-spec-template.md
```

## Installation

Hosted at **https://github.com/relevantzgit/software-engineering-system**. On Claude Code
2.1.275 or later, install it in one step:

```
/plugin install feature-spec-authoring --marketplace relevantzgit/software-engineering-system
```

Or add the marketplace first, then install:

```
/plugin marketplace add relevantzgit/software-engineering-system
/plugin install feature-spec-authoring
```

To update later after the repo changes:

```
/plugin marketplace update software-engineering-system
/plugin install feature-spec-authoring
```

No configuration is required — the skill works with plain Markdown out of the box.

## Troubleshooting

- **The skill didn't trigger.** Name the artifact explicitly — "write a *feature spec* for …"
  or "turn this into *requirements* with user stories." Very short, one-step asks may be
  handled without consulting the skill.
- **The spec came out too technical.** The skill writes for the business; if you want
  implementation detail, ask for it separately — it is deliberately out of the spec body.
- **A section is `N/A`.** That is intentional when a section doesn't apply; the heading is
  kept so readers know it was considered.

## Privacy & data handling

The skill collects and transmits **no data**. It reads only the content you give it in the
conversation and writes a Markdown spec. No remote calls, logging, or storage.

## Optional: tool-backed authoring

The skill is tool-agnostic. If — and only if — your organisation already runs a
requirements/governance system exposed over MCP, and you ask Claude to use it, the skill can
read your decision log or access matrix from that system and register the spec through it.
That MCP server is **configured separately by you and is not bundled with, started by, or
required by this plugin.** Without it, the skill works fully in plain Markdown.

## Support & contact

- **Product & general support:** chandra.perumal@relevantz.com
- **Security reports:** see [SECURITY.md](SECURITY.md)
- Issues are addressed within a reasonable timeframe; the skill is actively maintained.

## License

See [LICENSE](LICENSE).

## Version

0.1.0 — first release.
