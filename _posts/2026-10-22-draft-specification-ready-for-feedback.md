---
layout: post
title: "The OpenLint specification draft is ready for feedback"
author: Kin Lane
image: /assets/blog/2026-10-22-draft-spec.jpg
image_alt: "Pill-shaped figures reviewing a two-page document of rule bars, with a mint-green squiggle resolving into a check mark above"
summary: "The first formal draft of the OpenLint Ruleset Specification is published at spec.openlint.org, with 94 numbered requirements, conformance tests, and 36 open questions we'd like your help with."
crumbs:
  - name: blog
    url: /blog/
---

The first formal draft of the **OpenLint Ruleset Specification** is published at **[spec.openlint.org](https://spec.openlint.org)**, and we'd like your feedback.

Rulesets are how teams write down their API style guides and governance: thousands of them already exist in the Spectral format. But that format was never specified; it was whatever one tool did. This draft changes that. It describes the ruleset format as it works today, so existing rulesets stay valid, and writes it down as a proper specification that any tool can implement.

## What's in the draft

Joost Farla rewrote the specification as a formal [Working Draft](https://spec.openlint.org/v1/draft/), built with Bikeshed, the tool behind many W3C-style specifications:

- **94 numbered requirements**, each written as a testable MUST, SHOULD or MAY, and each aimed at either a ruleset or a linter
- **Conformance tests** listed for each requirement, so any linter can check that it behaves the same way
- Chapters on **the ruleset format, documents, linting and functions**, plus a **security and privacy** section
- A machine-readable [requirements index](https://spec.openlint.org/v1/draft/requirements.json) and the [JSON Schema](https://spec.openlint.org/v1/ruleset.schema.json) for tooling
- A version line: the working draft now, with versioned releases to follow

## Where we need help

Writing the format down surfaced a lot of behavior that was never documented, only implemented. The draft marks **36 open questions** inline, right where they occur. For example, a YAML file with several documents is accepted today, but only the first one is linted. Should it be?

These are exactly the decisions that need more than one voice:

- **Read the draft** at [spec.openlint.org](https://spec.openlint.org) and look for the open questions in your area
- **Comment** in [discussion #13](https://github.com/orgs/openlint/discussions/13), or open an issue in [openlint/spec](https://github.com/openlint/spec/issues)
- **Bring your rulesets**: if a ruleset you rely on behaves differently from what the draft says, that's the most useful report you can send

Under our [governance](https://github.com/openlint/community/blob/main/GOVERNANCE.md), changes to the specification stay open for at least 14 days, and anything breaking for 30, with known implementers told directly. Nothing here changes what your rulesets do today.

Join us at [office hours](/meetings/) on Thursdays if you'd rather talk it through.

*Drafted with Claude, and edited by me.*
