---
layout: post
title: "Migrating from Spectral to OpenLint: we're looking for beta testers"
author: Kin Lane
image: /assets/blog/2026-10-29-migration-beta.jpg
image_alt: "Pill-shaped figures carrying boxes across a bridge from a dim platform to a bright one, where one figure waves the others on, under a mint-green squiggle resolving into a check mark"
summary: "API Commons has moved from Spectral to OpenLint without changing its results. Now we want companies, organizations, institutions and government agencies to try the migration and tell us what breaks."
crumbs:
  - name: blog
    url: /blog/
---

OpenLint 1.0.0 is on npm, the [specification](https://spec.openlint.org) is published, and the [docs](https://docs.openlint.org/getting-started/) are live. The next step is the one that matters most to anyone running Spectral today: moving over. We're looking for beta testers to help us prove that path.

## API Commons has switched

API Commons runs a stack of API governance tools on the linter, including [validator.apicommons.org](https://validator.apicommons.org), a governance MCP server and a catalog of more than 700 rules. All of them now run on OpenLint. We checked the results against Spectral 6.16.1 on every fixture we have, and they matched.

The move was mostly a rename. What tripped us up is what we want to hear about from you:

- **Custom functions that import Spectral's core.** A function that imports `@stoplight/spectral-core` won't load in OpenLint. Import from `@openlint/openlint-core` instead, and use named imports rather than a default import.
- **Extra metadata on rules.** Rulesets that carry their own properties, such as a title or a prompt for an AI agent, are rejected, so we strip them from published rulesets for now.
- **JSON output on a clean run.** With `-f json`, a run with no problems prints `[]` plus a line of text, which a script parsing the output has to allow for.

These are in front of the community, and backwards compatibility is the subject of an [open discussion](https://github.com/orgs/openlint/discussions/12).

## How to migrate

The [Spectral migration guide](https://docs.openlint.org/migration-guides/spectral/) has the details. For most teams it's two steps:

1. Install OpenLint: `npm install openlint`, or run it with `npx openlint lint`.
2. Change `spectral` to `openlint` in your commands and pipelines.

Your existing `.spectral.yaml` and `extends: spectral:oas` keep working. If you use the JavaScript API, the guide shows how to alias the old package names so you can try OpenLint without changing any code, and how to rename things properly when you're ready.

## Help us test it

We want companies, organizations, institutions and government agencies of every size to try the migration on their real rulesets and pipelines: custom functions, shared rulesets pulled over the network, CI setups, and editor workflows.

If you'd like to take part:

- **Tell us you're testing.** Email [info@openlint.org](mailto:info@openlint.org) or start a thread in [Discussions](https://github.com/orgs/openlint/discussions). Just knowing who's trying it helps us decide what to fix first.
- **Report what breaks.** Anything that behaves differently from Spectral, or anything the guide doesn't cover, goes in [an issue on openlint/openlint](https://github.com/openlint/openlint/issues).
- **Come to office hours.** We meet every Thursday at 9:00 ET. Agendas are in [openlint/community](https://github.com/openlint/community/issues?q=label%3Ameetings), and [recordings and transcripts](/meetings/) are on this site.

We're aiming to make the official launch at API Days Paris, and we'd like to go in with migration stories from more than one organization. If yours could be one of them, we'd love to hear from you.
