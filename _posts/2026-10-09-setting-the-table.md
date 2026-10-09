---
layout: post
title: "Setting the table: the second OpenLint office hours"
author: Kin Lane
image: /assets/blog/2026-10-09-setting-the-table.jpg
image_alt: "Pill-shaped figures setting a long table with lines of code, a mint-green squiggle resolving into a check mark at its head"
summary: "Office Hours #2 was about getting OpenLint open for business: the specification up for review, the code renamed and cleaned up, and a growing list of people doing the work."
crumbs:
  - name: blog
    url: /blog/
---

We held the second OpenLint office hours on 8 October. The [recording, summary and full transcript](/meetings/office-hours/2026-10-08/) are up, and the [agenda is on GitHub](https://github.com/openlint/community/issues/26).

The theme this week was setting the table. Our goal right now isn't new features. It's getting OpenLint open for business: running on par with Spectral, with governance, so the people who depend on it can switch.

## The specification

The specification and its JSON Schema are up for review in [openlint/spec#2](https://github.com/openlint/spec/pull/2). It documents the ruleset format as it works today, without changing it. If you have feedback, now is the time; we'll merge in a couple of weeks.

Backwards compatibility took most of the hour. Everyone agrees that every ruleset that works in Spectral today has to keep working. Jakub Rożek pushed us further: compatibility also covers the JavaScript API that editors embed, and the lint results themselves, the same messages and ranges from the same ruleset. Measuring that takes a conformance suite, and that conversation continues in [discussion #12](https://github.com/orgs/openlint/discussions/12). We also need to decide what our first version number is.

## The code

Telemetry is gone. Phil Sturgeon's rename and cleanup merged in [openlint#1](https://github.com/openlint/openlint/pull/1) and continues in [#6](https://github.com/openlint/openlint/pull/6). Jakub is upgrading Node in [#7](https://github.com/openlint/openlint/pull/7), and Miguel Quintero sent his first pull request, upgrading TypeScript, in [#8](https://github.com/openlint/openlint/pull/8). Next comes supply chain health, cleaning up vendorisms, and a migration path off Spectral.

## New discussions

People are bringing real needs to the table:

- Dimitri van Hees asks for [case-insensitive matching (#27)](https://github.com/orgs/openlint/discussions/27), so a rule can check for an `api-version` header without listing every spelling.
- Andrzej Jarzyna raises [custom functions and an expression language (#28)](https://github.com/orgs/openlint/discussions/28), so rulesets don't have to run someone else's JavaScript.
- Andrzej also proposes [comparing two versions of a document (#29)](https://github.com/orgs/openlint/discussions/29) to catch breaking changes.

## Running the project

Proposals for [governance](https://github.com/openlint/community/pull/17) and a [maintainers page](https://github.com/openlint/community/pull/21) are open, and everyone who comes to office hours is listed as a contributor. We're on [Open Collective](https://opencollective.com/openlint), waiting on Open Source Europe to accept us as our fiscal host. I'm also drafting a simple way to disclose AI use on issues and pull requests, rated from 1 (none) to 5 (fully automated). This post was drafted with Claude; I'd rate it a 4.

## Get involved

The [roadmap](/roadmap/) shows what's in progress and what's still unclaimed, and the [changelog](/changelog/) shows what moved each week. Pick something up, start a [discussion](https://github.com/orgs/openlint/discussions), or join us at office hours on Thursday.
