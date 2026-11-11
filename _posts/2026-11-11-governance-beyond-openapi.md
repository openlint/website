---
layout: post
title: "The governance layer Europe's API standards are missing"
author: Kin Lane
image: /assets/blog/2026-11-11-beyond-openapi.jpg
image_alt: "Several separate islands, each with its own small checking machine and pill-shaped figures, connected by a mint-green squiggle line that resolves into a check mark"
summary: "Europe's public data runs on many standards (OGC, SDMX, NeTEx, GTFS, DATEX II, DCAT-AP), each with its own validator. What's missing is a shared, open layer for the rules governments write on top. That's the opportunity beyond OpenAPI."
crumbs:
  - name: blog
    url: /blog/
---

OpenLint's starting point is OpenAPI. But in getting ready for the EU government track at [APIdays Paris](https://www.apidays.global/) this December, I've spent a lot of time with the standards Europe's public sector actually runs on, and OpenAPI is only one of them.

## Europe runs on many standards

When you sample the APIs and services that European governments report for the [High-Value Datasets regulation](https://eur-lex.europa.eu/eli/reg_impl/2023/138/oj), a picture of sector standards comes out:

| Standard | Where it's used | How it's checked today |
|---|---|---|
| **OpenAPI** | general REST APIs, and the OGC API generation | rulesets, written agency by agency |
| **OGC API** (Features, Records…) | next-generation geodata | OGC TEAM Engine test suites |
| **OGC WMS / WFS / WCS** | geodata under INSPIRE, by far the most common | OGC conformance tests, INSPIRE Reference Validator |
| **INSPIRE Atom** | download services | INSPIRE Reference Validator |
| **SDMX** | official statistics | SDMX validation tools |
| **PxWeb / JSON-stat** | statistics, especially in the Nordics | JSON-stat schema |
| **NeTEx, SIRI, GTFS** | public transport, national access points | GTFS validators, NeTEx schemas and profiles |
| **DATEX II** | roads and traffic | DATEX II schemas |
| **DCAT-AP** | the national data catalogs themselves | SHACL shapes |
| **NGSI-LD** | smart cities | ETSI conformance tests |

Each of these standards has a community, a schema, and usually a validator. That's real, hard-won work.

## What each validator answers, and what it doesn't

A validator answers one question: does this document or service conform to the standard? It's necessary, and it isn't governance.

Governance is everything a public body decides on top of the standard. How we name things, which version we use, how we describe errors and authentication, what a developer has to find before they can start, which profile of NeTEx we publish, what our DCAT-AP records must always include. Today those decisions live in PDFs, wikis and people's heads, and checking them is manual. Where they are machine-checkable, they're locked inside one tool for one standard.

So a government that publishes OpenAPI, OGC services, SDMX and DCAT-AP ends up with four different ways of checking its own rules, or none.

## What OpenLint can offer beyond OpenAPI

The OpenLint ruleset format is about rules over structured documents: JSONPath to select, functions to test, severities and messages for people. That's not specific to OpenAPI. Spectral rulesets already lint AsyncAPI and arbitrary JSON and YAML, and the [specification](https://spec.openlint.org) is being written to describe that format on its own, so any tool can implement it.

Here's where that could go:

- **One way to write down public-sector API rules,** whatever standard the document follows, so a government's design rules can sit in one place and be checked in one pipeline.
- **Shared rulesets per standard,** written in the open by the people who run them: a common baseline for OGC API definitions, for DCAT-AP records, for the JSON and YAML around NeTEx and GTFS feeds.
- **Rules that sit next to the existing validators, not instead of them,** so conformance stays with each standard's community and governance gets a common home.

None of this is decided. It's an open question for the community, and it's the conversation I want to have with government teams in Paris.

## Bring it to Paris, or to office hours

If your team publishes data under one of these standards and checks it by hand, I'd like to hear what you check and how. Find us at [APIdays Paris](https://www.apidays.global/) in December, come to [office hours](/meetings/) on Thursdays, or start a thread in [Discussions](https://github.com/orgs/openlint/discussions). Tell us which standard you'd want rulesets for first.
