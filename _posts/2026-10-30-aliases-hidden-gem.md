---
layout: post
title: "Aliases: the hidden gem in OpenLint"
author: Kin Lane
image: /assets/blog/2026-10-30-aliases.jpg
image_alt: "Pill-shaped figures following long, tangled lines that a small signpost gathers into one straight route, ending in a mint-green squiggle resolving into a check mark"
summary: "Aliases let you name a JSONPath once and use that name in every rule. They work in OpenLint today, few people talk about them, and they take much of the pain out of writing rulesets."
crumbs:
  - name: blog
    url: /blog/
---

Ask people what's hard about writing API rulesets and JSONPath comes up quickly. It came up again at [Office Hours #5](/meetings/). Deciding what a rule should check is usually the easy part. Working out the path that selects every place it applies is the hard part, and then you have to repeat that path in every rule.

OpenLint already has an answer to this, and it doesn't get much attention. Aliases work today, in the version on npm, with nothing to install or turn on.

## Name it once

An alias gives a name to one or more JSONPath expressions. Here are two rules without one:

```yaml
rules:
  operation-summary:
    given: $.paths[*][get,put,post,delete,options,head,patch,trace]
    then:
      field: summary
      function: truthy
  operation-tags:
    given: $.paths[*][get,put,post,delete,options,head,patch,trace]
    then:
      field: tags
      function: truthy
```

And here are the same two rules with one, reporting exactly the same problems:

```yaml
aliases:
  Operation:
    - $.paths[*][get,put,post,delete,options,head,patch,trace]
rules:
  operation-summary:
    given: "#Operation"
    then:
      field: summary
      function: truthy
  operation-tags:
    given: "#Operation"
    then:
      field: tags
      function: truthy
```

Now the rule reads as what it means: every operation needs a summary. Someone can write or review it without being able to read the path, and the path lives in one place, where the person who knows JSONPath can get it right once.

## Change it once

That one place pays off when the format moves. OpenAPI 3.2 added a `query` method, and the path above doesn't select it, so an operation using it passes both rules without being checked. With the path copied into every rule, you'd have to find and fix each copy. With an alias, you add `query` to one line and every rule picks it up. We tried it: the same document went from no problems to two.

## Say what you actually mean

A single alias can hold several paths, which is where it gets really useful. Say you want every server URL to use https. You could reach for `$..servers`, but that also matches any property named `servers` in a schema or an example. So list the real locations and give them a name:

```yaml
aliases:
  Servers:
    - $.servers[*]
    - $.paths[*].servers[*]
    - $.paths[*][get,put,post,delete,options,head,patch,trace].servers[*]
    - $..callbacks[*][*].servers[*]
    - $..callbacks[*][*][get,put,post,delete,options,head,patch,trace].servers[*]
rules:
  server-https:
    message: "{% raw %}{{value}}{% endraw %} must use https"
    given: "#Servers.url"
    then:
      function: pattern
      functionOptions:
        match: "^https://"
```

Notice `#Servers.url`. You can carry on with more path after the name, and aliases can be built from other aliases, so a small set of well-named building blocks can serve a whole ruleset. This rule is also in the registry as [server-https](https://rules.openlint.org/server-https/).

## One name across versions

The same thing often lives in different places in different versions of a format. Reusable parameters are at `$.parameters` in Swagger 2.0 and `$.components.parameters` in OpenAPI 3. A scoped alias picks its paths by the format of the document being linted:

```yaml
aliases:
  ParameterObject:
    targets:
      - formats: [oas2]
        given:
          - $.parameters[*]
      - formats: [oas3]
        given:
          - $.components.parameters[*]
```

A rule that uses `#ParameterObject` doesn't need to know which version it's looking at, as long as it lists the same `formats`. The version differences stay inside the alias.

## Where they stop

Aliases have limits you should know about. The big one is that an alias belongs to the ruleset that declares it. `spectral:oas` has a good `OperationObject` alias, but extending that ruleset doesn't let your rules use it, so for now you copy what you need. Everyone ends up writing their own `Servers`, and nothing helps you share them.

That's an opportunity as much as a limit. Whether aliases should be shareable is an open question in the [specification](https://spec.openlint.org/v1/draft/#aliases) and in [discussion #2](https://github.com/orgs/openlint/discussions/2), and shared, tested aliases for each format could take a lot of JSONPath off the plate of everyone writing rules. If you have opinions, please bring them there.

## Try it

Next time you paste a path into a second rule, make it an alias. Our [aliases guide](https://learn.openlint.org/aliases/) covers all of this, including the limits and a YAML gotcha that produces a confusing error, and every example in it was run against OpenLint 1.0.0.

If you've already written good aliases for your own rulesets, we'd love to see them. Share them in [Discussions](https://github.com/orgs/openlint/discussions) or bring them to [office hours](/meetings/) on Thursdays.
