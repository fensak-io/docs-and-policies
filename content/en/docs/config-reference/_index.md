---
title: Config file reference
description: A reference overview of the Fensak config file
no_list: true
weight: 30
---

The Fensak configuration file is a static config file in the `.fensak` repository of your Organization that specifies
which rules should be run on PRs for your repositories. This document contains information about the config file,
including the schema of the config, what types are supported, how updates are handled, and some considerations for
rules.

## File location

The Fensak config file is expected to be located at the root of the `.fensak` repository in your Organization. The
config file must also be named exactly as one of the specific names mentioned in [Supported config file
types](#supported-config-file-types), depending on what file type is used.


## Schema

We offer a [JSON schema](https://json-schema.org/) of the config format at
[fensak-io/fensak/fskconfig/schema.json](https://github.com/fensak-io/fensak/blob/main/fskconfig/schema.json). Refer to
the schema file for information on what options are available, what they are, and any restrictions on supported values.

You can also use a tool like [ajv-cli](https://www.npmjs.com/package/ajv-cli) to validate your configuration against the
provided schema to make sure it conforms.


## Supported config file types

The following file types are supported for the Fensak config:

- YAML (as `fensak.yml` or `fensak.yaml`)
  ```yaml
  repos:
    my-repo:
      ruleFile: rules/sample.ts
      ruleLang: ts
      requiredReviews: 1
  ```

- JSON (as `fensak.json`)
  ```json
  {
    "repos": {
      "my-repo": {
        "ruleFile": "rules/sample.ts",
        "ruleLang": "ts",
        "requiredReviews": 1
      }
    }
  }
  ```


- TOML (as `fensak.toml`)
  ```toml
  [repos]
  [repos.my-repo]
  ruleFile = "rules/sample.ts"
  ruleLang = "ts"
  requiredReviews = 1
  ```


## Updates and eventual consistency

The config file is loaded directly from the `.fensak` repository and is cached by the git SHA of the head commit on the
default branch. The config is loaded asynchronously, and is eventually consistent within Fensak. This means that you may
see a delay between updating the config (or rules) in the `.fensak` repository. If you see issues with Fensak checks not
appearing on PRs for new repositories, you can force a retry by submitting a review comment on the PR.


## What if I want to bind multiple rules to a repository?

Fensak only supports a single rule script to run on PRs in a repository. This is to keep the config file logic simple,
but also because we find it difficult to specify complex rules in a static configuration DSL (e.g., do you mean `all` or
`any`? What about only `and` on some rules and `or` for others?). This is better suited for a full programming logic
like JavaScript.

As such, we recommend encoding multi-rule rules in the rule function itself. This allows you to use any arbitrary
JavaScript based boolean algebra to decide how to combine your independent rules function. You can even modularize your
code to improve maintainability, although this will require an extra compile step from a bundler that outputs a single
JS file for the rule with all the functions concatenated.
