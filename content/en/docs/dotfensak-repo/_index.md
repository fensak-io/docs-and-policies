---
title: The .fensak repository
description: A reference overview of the .fensak configuration repository
no_list: true
weight: 15
---

All Fensak configuration is managed through a special repository in your GitHub Organization: the `.fensak` repository.
This repository should contain your auto-approval rules and the mapping configuration for which rules apply to which
repos. We use this repository for configuring Fensak in lieu of a UI so that you don't need to manage yet another
account for a service.

This guide provides an overview of the `.fensak` repository and what is expected to be included in it.

## Template repositories

To make it easy to get started, we offer template repositories that contain everything needed to
configure the `.fensak` repo. We recommend creating the `.fensak` repository in your Org by using the template repo. Refer to
the [official GitHub
documentation](https://docs.github.com/en/repositories/creating-and-managing-repositories/creating-a-repository-from-a-template)
for instructions on how to use a template repo.

Here are the template repositories that we currently have available:

- [fensak-io/dotfensak-deno-template](https://github.com/fensak-io/dotfensak-deno-template): TypeScript based rules and
  tests, using [Deno](https://deno.com/) as the testing/linting runtime.
- [fensak-io/dotfensak-jest-template](https://github.com/fensak-io/dotfensak-jest-template): JavaScript based rules and
  tests, using [Node](https://nodejs.org/en) with [Jest](https://jestjs.io/) as the testing runtime, and
  [ESLint](https://eslint.org/) + [Prettier](https://prettier.io/) as the linting runtime.
- [fensak-io/dotfensak-ts-jest-template](https://github.com/fensak-io/dotfensak-ts-jest-template): TypeScript based
  rules and tests, using [Node](https://nodejs.org/en) with [Jest](https://jestjs.io/) as the testing runtime, and
  [ESLint](https://eslint.org/) + [Prettier](https://prettier.io/) as the linting runtime.

You can use any one of the template repositories to kick start your `.fensak` repo.

Refer to the [Create a .fensak
repository](/docs/getting-started/#create-a-fensak-repository-in-your-github-organization) section of the `Getting
started guide` for specific instructions on how to use the template.


## The config file

The main file in the `.fensak` repository is [the config file](/docs/config-reference), which maps your Organization
repositories to the rules that should be evaluated against the pull requests. Only repositories that are specified in
the config file are monitored by Fensak.

The config file is the only file that has requirements on the general structure of the repository. This file must be
located at the root of the repository, and must be named `fensak.EXT` where `EXT` can be any of the supported file types
(`json`, `yml`, `toml`).

Refer to the [Config file reference](/docs/config-reference) for more details.


## Rules scripts

The `.fensak` repository should hold the auto-approval rules scripts that you want evaluated against pull requests in
your Organization. The rules scripts can be located anywhere in the repo, in arbitrary subfolders, as long as the path
matches that which is specified in the config file.

Refer to the [Writing rules guide](/docs/writing-rules) for more information on writing your rules.
