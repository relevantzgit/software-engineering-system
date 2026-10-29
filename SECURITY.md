# Security Policy

## Reporting a vulnerability

If you discover a security issue in this plugin, please report it privately to:

**chandra.perumal@relevantz.com** (subject line: `SECURITY — feature-spec-authoring`)

Please include:
- a description of the issue and its potential impact,
- steps to reproduce,
- the plugin version affected (see `.claude-plugin/plugin.json`).

We aim to acknowledge reports within a reasonable timeframe, investigate with reasonable care,
and address confirmed issues in a timely manner. This channel is open to Anthropic and to
third parties.

## Scope

This plugin ships only a Skill (Markdown instructions and a template). It executes no code,
starts no server, and transmits no data. Security reports will typically concern the content
of the instructions (for example, wording that could cause unintended behaviour) rather than
runtime vulnerabilities.
