---
layout: post
title: "Europe's next generation of geodata APIs speaks OpenAPI"
author: Kin Lane
image: /assets/blog/2026-11-11-geodata-openapi.jpg
image_alt: "Pill-shaped figures carrying stacked map tiles across a bridge from an old grid of layers toward a clean contract document, with a mint-green squiggle resolving into a check mark at the far end"
summary: "Europe's High-Value Datasets are overwhelmingly served through the classic OGC services. The OGC API standards replacing them are described in OpenAPI by design, so as Europe's geodata migrates, it lands in OpenAPI governance."
crumbs:
  - name: blog
    url: /blog/
---

Preparing my keynote for the EU government track at [APIdays Paris](https://www.apidays.global/) this December, I wanted to see what the law asks of public APIs, what governments report, and what actually answers when you call it. The [High-Value Datasets regulation](https://eur-lex.europa.eu/eli/reg_impl/2023/138/oj) is the clearest test we have. It names six categories (geospatial, earth observation and environment, meteorological, statistics, companies, and mobility) that public bodies must make available as open data, including through APIs.

Member states report those datasets to [data.europa.eu](https://data.europa.eu/), so you can count them.

## Europe's open data runs on OGC

When I pulled the reported High-Value Datasets in November, there were about 29,600 of them. Their distribution formats tell you which standards Europe runs on:

- **OGC Web Map Service (WMS):** about 19,100
- **OGC Web Feature Service (WFS):** about 4,800
- **INSPIRE Atom feeds:** about 1,100
- **OGC Web Map Tile Service:** about 330
- **OGC API – Features:** about 390

OpenAPI isn't in the top forty formats. That makes sense. INSPIRE built Europe's spatial data infrastructure on the classic OGC services long before most of us were writing OpenAPI, and the High-Value Datasets regulation builds on INSPIRE.

## The next generation is OpenAPI-described

The OGC API family of standards is replacing those services: [Features](https://ogcapi.ogc.org/features/), Records, Tiles, Maps, Processes and more. They're resource-oriented web APIs, and they describe themselves in OpenAPI. OGC API – Features includes an OpenAPI conformance class, and the common implementations serve an OpenAPI definition at a known path.

I saw that in the data. I sampled 893 reported High-Value Dataset endpoints across Europe and called each one. Seven declared themselves as OpenAPI. Six of those seven were OGC API – Features services, a geoserver describing its feature collections in OpenAPI. The OpenAPI in Europe's legally mandated open data is arriving through geodata.

## Why that matters for governance

The classic OGC services have conformance tests: OGC's [TEAM Engine](https://cite.opengeospatial.org/teamengine/) and the [INSPIRE Reference Validator](https://inspire.ec.europa.eu/validator/). They tell you whether a service implements a standard. They don't tell you whether a public body's APIs are consistent with each other, follow its national design rules, or are written so a developer, or an agent, can use them without a phone call.

That's the question rulesets answer, and it's the work OpenLint does. As agencies move their geodata to OGC API, their OpenAPI definitions can be linted like any other contract. That includes the Dutch API Design Rules, which already cover geospatial APIs, and any shared rules for OGC API that the community writes down.

## Let's talk in Paris

If you run a national spatial data infrastructure, a geoportal, or the migration from WMS and WFS to OGC API, I'd like to hear how you check what you publish. I'll be at [APIdays Paris](https://www.apidays.global/) in December with the EU government track. Before then, come to [office hours](/meetings/) on Thursdays or open a thread in [Discussions](https://github.com/orgs/openlint/discussions). A shared, open ruleset for OGC API would be a good thing to start there.
