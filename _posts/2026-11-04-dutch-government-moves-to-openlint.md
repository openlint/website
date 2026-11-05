---
layout: post
title: "The Dutch government's developer portal now runs on OpenLint"
author: Kin Lane
image: /assets/blog/2026-11-04-dutch-government.jpg
image_alt: "Pill-shaped figures carrying API documents along an Amsterdam canal, past gabled houses, bicycles and a bridge, toward a mint-green squiggle resolving into a check mark"
summary: "developer.overheid.nl has switched all of its tooling, including the DON Checker, from Spectral to OpenLint. Their rulesets for the API Design Rules, OpenAPI, publiccode.yml and JSON-FG work without changes. An English translation of what they wrote."
crumbs:
  - name: blog
    url: /blog/
---

This week [developer.overheid.nl](https://developer.overheid.nl/), the developer portal of the Dutch government, moved all of its tooling to OpenLint. Dimitri van Hees and Joost Farla wrote about it in Dutch: [Het is zover: OpenLint vervangt Spectral](https://developer.overheid.nl/blog/2026/11/04/openlint-vervangt-spectral) ("It's happening: OpenLint replaces Spectral"). Here's what they said, in English, and why it matters to the rest of us.

## What they did

> "As of this week, all developer.overheid.nl tooling runs on OpenLint, the successor to Spectral. We've been actively involved since July, both in the specification of the ruleset format and in the discussions about the direction of the project. When version 1.0 came out recently, we switched our tooling over straight away, including the DON Checker. The rulesets we wrote for the API Design Rules (ADR), and for validating OAS, publiccode.yml and JSON-FG, work without any changes."

The [API Design Rules](https://gitdocumentatie.logius.nl/publicatie/api/adr/) are the Dutch government's standard for REST APIs, maintained by Logius. Spectral is written into the standard itself, so this isn't a small team swapping a dev dependency. It's a national API standard moving its reference tooling to OpenLint, and its rulesets running unchanged on it.

## Why they moved

Dimitri and Joost tie it back to [their July post](https://developer.overheid.nl/blog/2026/07/31/spectral-onder-vuur), written after the 14 July supply chain incident, when two malicious versions of `@asyncapi/specs`, a Spectral dependency, were published to npm:

> "Anyone who did a fresh install in that window pulled in code that could exfiltrate SSH keys, tokens and credentials, among other things. The incident itself was resolved quickly, but the issue about it on the Spectral repository stayed silent. For many users that was the last straw, because hundreds of issues were already open and bugs in the VS Code plugin had gone unaddressed for a long time."

They didn't rip Spectral out in a hurry. They pinned it, and looked at [vacuum](https://quobix.com/vacuum/), but it doesn't fully support the ruleset format, is maintained in practice by one person, and is written in Go, while their tooling also has to run in the browser. So they helped build the fork that started under API Commons instead:

> "For everyone who lay awake all summer over 'Spectralgate' wondering what the sensible next steps were, OpenLint is now the answer."

## The specification is the part I want to point at

Their biggest contribution isn't the switch. It's the [specification](https://spec.openlint.org/v1/draft/):

> "With Spectral, the ruleset format was nothing more than whatever the linter accepted in practice. We rewrote the format from the existing Spectral code into a specification of its own, published with ReSpec, with a JSON Schema and requirements stated in terms of MUST and SHOULD. That separates the specification from the toolbox, so any linter can implement the format, and OpenLint is one of them."

They go further, and I agree with every word of it:

> "Ideally vacuum becomes a Go implementation of that specification, so that a ruleset gives the same result everywhere, whichever linter you use."

They also want OpenLint to lint more than OpenAPI, AsyncAPI and Arazzo, including Dutch government standards such as NL-SBB and [DCAT-AP-NL](https://docs.geostandaarden.nl/dcat/dcat-ap-nl30/). That's the work we're scoping in [openlint#40](https://github.com/openlint/openlint/issues/40): new formats without breaking changes, and rulesets for standards.

And on where the project lives:

> "In July we said we'd help find a place to land, because a fork isn't yet a standard. We found that place at Open Source Europe, where OpenLint will be hosted. That puts the format the ADR ruleset is written in into European public hands."

## How to switch, the way they describe it

If you call Spectral directly, swap the package and the command. Your rulesets don't need converting, and an existing `.spectral.yaml` is still picked up. New projects can use `.openlint.yaml`.

```diff
- npm install --save-dev @stoplight/spectral-cli
+ npm install --save-dev openlint

- npx spectral lint openapi.yaml
+ npx openlint lint openapi.yaml
```

If you call the linter from your own code, the import and the class name change. `RulesetDefinition` and your ruleset stay the same.

```diff
- import { Spectral, type RulesetDefinition } from "@stoplight/spectral-core";
+ import { OpenLint, type RulesetDefinition } from "@openlint/openlint-core";
```

For Dutch government APIs they recommend the [DON Checker](https://github.com/developer-overheid-nl/don-checker), which wraps the ADR and publiccode.yml checks and keeps the linter and rulesets up to date for you:

```bash
npx @developer-overheid-nl/don-checker@latest \
  validate --standard adr --input ./openapi.json
```

## What they're taking on next

- **Editors:** a language server for OpenLint, so the linter works in every IDE without a separate plugin per editor. That's the work in [discussion #9](https://github.com/openlint/community/discussions/9) and [openlint/language-server](https://github.com/openlint/language-server).
- **vacuum:** mapping where it differs from OpenLint. Most differences come from Spectral's JavaScript legacy in regular expressions and JSONPath, and "on some points vacuum follows the underlying standards better than Spectral."
- **A new version of the specification:** backwards compatible with existing rulesets, written so a ruleset works the same in OpenLint and in vacuum, and open to formats beyond OpenAPI, AsyncAPI and Arazzo.
- **Education:** tutorials and reusable aliases for common `given` paths and regular expressions. If you haven't seen them, [aliases already do a lot of this today](/blog/2026/10/30/aliases-hidden-gem/).
- **Backwards compatibility:** testing that existing rulesets, ADR included, keep working with every change to the spec and toolbox.

## What this means for OpenLint

A government that wrote a linter into its own API standard has moved to OpenLint, contributed the specification that makes OpenLint more than one tool, and committed people to the roadmap. We're aiming for the official launch on 3 December in the Europe API track at apidays Paris, but as Dimitri and Joost say, you don't have to wait: version 1.0 is out and you can use it now.

Thank you, Dimitri and Joost, and the developer.overheid.nl team at Geonovum. Read [the original post in Dutch](https://developer.overheid.nl/blog/2026/11/04/openlint-vervangt-spectral), try OpenLint, and join us at [office hours](https://github.com/openlint/community) on Thursdays.

*The quotes are our English translation of the original Dutch post.*
