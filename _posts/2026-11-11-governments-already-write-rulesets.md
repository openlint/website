---
layout: post
title: "Europe's governments are already writing API rulesets. Separately."
author: Kin Lane
image: /assets/blog/2026-11-11-governments-rulesets.jpg
image_alt: "Separate small stacks of rule bars scattered across a dark background, with one mint-green squiggle running through all of them and resolving into a check mark"
summary: "Ahead of APIdays Paris, I looked at how European public bodies govern their APIs. At least seven already publish their own Spectral rulesets: national design rules, platform guidelines, single services. Each one maintains its own. That is the case for OpenLint."
crumbs:
  - name: blog
    url: /blog/
---

I'm getting ready for [APIdays Paris](https://www.apidays.global/) in December, where I'm moderating the EU government track and giving its keynote on what Europe's government APIs look like from the outside, the way a developer, a business or an AI agent meets them. Part of that work has been reading the public API surfaces of about 170 government agencies, ministries and public platforms across Europe. One thing stood out, and it belongs here first.

## Governments already govern their APIs with rulesets

When a public body takes API governance seriously, it reaches for the same tool. Here are rulesets I found published in public bodies' own repositories, all in the Spectral format OpenLint carries forward:

- **Logius** maintains the Dutch government's [API Design Rules](https://github.com/Logius-standaarden/API-Design-Rules), and ships a Spectral linter with them. As [we wrote last week](/blog/2026/11/04/dutch-government-moves-to-openlint/), developer.overheid.nl now runs that tooling on OpenLint.
- **VNG Realisatie**, which builds shared services for Dutch municipalities, keeps a ruleset in [Haal-Centraal-common](https://github.com/VNG-Realisatie/Haal-Centraal-common) for the Haal Centraal APIs.
- **Entur**, Norway's national public transport platform, publishes its [API guidelines](https://github.com/entur/api-guidelines) with a Spectral ruleset alongside.
- **PagoPA**, the Italian state company behind pagoPA, the IO app and the PDND interoperability platform, lints contracts in repositories like [pn-mandate](https://github.com/pagopa/pn-mandate) and [interop-be-monorepo](https://github.com/pagopa/interop-be-monorepo).
- **Developers Italia** built its [OAS checker](https://github.com/italia/api-oas-checker) for the Italian public administration's interoperability guidelines on the Spectral engine.
- **publiq**, which runs Flanders' culture and leisure data platform, keeps rulesets per API in its [API docs](https://github.com/cultuurnet/apidocs).
- **HM Courts & Tribunals Service** in the UK lints at least some of its API contracts in the repository, for example [this crime hearing results API](https://github.com/hmcts/api-cp-crime-hearing-results-document-subscription).

That's seven public bodies in five countries. It's a floor, not a census, because I only counted what I could trace to the body's own repository.

## Each one is on its own

Every one of these rulesets is maintained separately. Most of them encode the same handful of decisions: use OpenAPI 3, describe your errors, version consistently, document authentication, name things one way. Each team wrote those rules again, keeps them current again, and carries the risk of a tool it doesn't control.

That last part isn't theoretical. This summer's Spectral supply chain incident is why developer.overheid.nl moved. Every team on that list depends on the same format, and until OpenLint none of them had a say in where it went.

## What OpenLint changes

OpenLint gives this work a shared, vendor-neutral home:

- **A specified format.** The [ruleset specification](https://spec.openlint.org) means a ruleset gives the same result in every tool that implements it, so a national standard doesn't depend on one linter.
- **Rulesets that work unchanged.** The Dutch rulesets ran on OpenLint without changes. Every ruleset in that list should too, and we'd like to hear if one doesn't.
- **Sharing instead of rewriting.** Once the format is stable, the common rules can live in one open place, with each government layering its own on top.
- **A neutral home.** OpenLint is hosted by [Open Source Europe](/blog/2026/10/29/open-source-europe-fiscal-host/), so no single vendor holds it.

## Come find us in Paris

If your agency publishes API design rules, or lints contracts in a pipeline, I'd like to talk before or during [APIdays Paris](https://www.apidays.global/). Bring your ruleset. We'll run it on OpenLint and tell you what happens. Until then, you can [try the migration from Spectral](/blog/2026/10/29/migrating-from-spectral-beta-testers/), join [office hours](/meetings/) on Thursdays, or start a thread in [Discussions](https://github.com/orgs/openlint/discussions).
