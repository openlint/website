---
layout: post
title: "Almost ready for business: the third OpenLint office hours"
author: Kin Lane
image: /assets/blog/2026-10-16-ready-for-business.jpg
image_alt: "A pill-shaped figure sending packages along a conveyor, with a mint-green squiggle resolving into a check mark above"
summary: "Office Hours #3: a first release within days, a formal specification taking shape, Open Source Europe as our fiscal host, and a short list of what's left before teams can switch from Spectral."
crumbs:
  - name: blog
    url: /blog/
---

We held the third OpenLint office hours on 15 October, with me dialing in from Stockholm after the Nordic APIs Summit. The [recording is on YouTube](https://youtu.be/ZtJjr1HjFPA) and the [agenda is on GitHub](https://github.com/openlint/community/issues/33).

Our focus hasn't changed: set the table before adding anything new. This week the table is nearly set.

## A first release

Phil Sturgeon plans to publish **0.1.0** within days: the rename from Spectral, with the tests passing. Then 0.2.0 by next week, and a fully backwards-compatible **1.0** in a month or two, with a new core ruleset and an export named `Spectral`, so JavaScript users can switch packages and nothing else. Breaking changes wait for 2.0. Installing it will be as simple as `npm install openlint`.

## A formal specification

Joost Farla showed a prototype of the specification built with Bikeshed, the tool behind many W3C-style specs. Every rule is written as a testable requirement, each aimed at either a ruleset or a linter, with conformance tests listed alongside, versioned releases and a working draft. We agreed to publish it from the [spec repo](https://github.com/openlint/spec) on its own subdomain. The first version documents the format as it works today; modular rulesets get their own discussion.

## Funding

[Open Source Europe](https://opencollective.com/openlint) is now our fiscal host, so we can accept donations. API Evangelist is putting in the first $1,000, and I'm going after European Commission grants. The first things we'd fund are small, well-scoped pieces like the release pipeline and the docs site.

## What's left

- The npm package and its release pipeline
- A docs site built from the Markdown in the code repo
- The specification site
- A migration guide, which Phil has started
- Editor support for VS Code *and* IntelliJ, ideally through a language server

After that, the first new thing on the list is validating Markdown and agent skills ([openlint#11](https://github.com/openlint/openlint/issues/11)), the most common request I hear.

A few companies have offered to be early adopters and tell us what migrating is like. I'll be the first, switching my own tooling over as soon as 0.1.0 is out.

Next week's office hours start an hour earlier, and we'll alternate times after that so more people can join. Check the [roadmap](/roadmap/) for what's unclaimed, and come say hello.

*Drafted with Claude from the recording, and edited by me.*
