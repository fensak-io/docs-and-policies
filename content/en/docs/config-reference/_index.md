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

The following is an overview of the schema.

### Repo config map

The main entry in the Fensak config is the `repos` key. This contains a map from repos in your Organization to the
corresponding rules configuration. The key of the map should match a corresponding GitHub repository slug in your
Organization. For example, the following is a repository config for the repo `my-repo` in the Organization:

```yaml
repos:
  my-repo:
    ruleFile: rules/sample.ts
```

Each entry in the map supports the following fields:

**ruleFile**

The path (relative to the repo root) to the file to use for the auto-approve rules source. When omitted, there is no
auto-approval rule. At least one of `requiredRuleFile` or `ruleFile` is required.

**ruleLang** *(optional)*

The language that the rules source is written in. This must be one of:
- `es5`: Rules written in JavaScript ECMAScript 5.1.
- `es6`: Rules written in JavaScript ECMAScript 6.
- `ts`: Rules written in TypeScript.

When omitted, the language is derived from the source file extension. Note that we will always assume ES6 for js files.


**requiredRuleFile**

The path (relative to the repo root) to the file to use for the required rules source. Required rules are rules that all
PRs must pass for the check to pass. When omitted, there is no required rules. At least one of `requiredRuleFile` or
`ruleFile` is required.


**requiredRuleLang** *(optional)*

The language that the required rules source is written in. The behavior is the same as `ruleLang`.


**requiredApprovals** *(optional)*

The number of unique approvals from users with write access that are required to pass the check when the auto-approve rule fails.
Can be zero if `requiredRuleFile` is set.

When omitted, defaults to 1.


**requiredApprovalsForTrustedUsers** *(optional)*

The number of unique approvals from users with write access that are required to pass the check for pull requests opened
by trusted users when the auto-approve rule fails. Can be zero if `requiredRuleFile` is set.

When omitted, defaults to the value set in `requiredApprovals`.


**requiredApprovalsForMachineUsers** *(optional)*

The number of unique approvals from human users with write access that are required to pass the check for pull requests
opened by machine users (GitHub Apps, or any user labeled as a machine user in the machineUsers top level key) when the
auto-approve rule fails. Can be zero if `requiredRuleFile` is set.

When omitted, defaults to the value set in `requiredApprovals`.


### Machine Users (optional)

A list of user logins that map to machine users in your account. This should not include GitHub Apps, as those are
automatically labeled as machine users.

When omitted or empty, `requiredApprovalsForMachineUsers` will only apply to PRs opened by GitHub Apps.


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
