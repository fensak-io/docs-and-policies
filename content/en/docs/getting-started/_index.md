---
title: Getting started
description: Get started using Fensak
no_list: true
weight: 10
---

In this section we cover installing the Fensak GitHub App (with a Marketplace Plan) and the steps needed to get started
protecting your GitOps branches with support for Continuous Delivery.

## Install the Fensak GitHub App

The Fensak GitHub App can be purchased and installed in your GitHub Organization through the offering on the [GitHub
Marketplace](https://github.com/marketplace). When you install, you will start a 14-day free trial period, after which
you will be automatically charged by the GitHub Marketplace. The charge will appear on your GitHub Organization invoice.

> **NOTE**
>
> Fensak does not offer a free plan beyond the free trial. The Pro tier paid subscription listed on the [pricing
> page](https://fensak.io/#pricing) is required for continuous access.

When installing the App, you have [the option to restrict which repositories Fensak has access
to](https://docs.github.com/en/apps/using-github-apps/installing-a-github-app-from-a-third-party#difference-between-installation-and-authorization).
Ensure that Fensak has access to repositories that you want Fensak to monitor, in addition to the `.fensak`
repository in your Organization. It is a good practice to always restrict the repositories that third-party GitHub Apps
have access to to only those that are necessary for the App to function.

Once you subscribe on the GitHub Marketwplace and install the GitHub App, you are ready to get started using Fensak!

Let's define our first rule and link it to a repository.


## Create a .fensak repository in your GitHub Organization

All Fensak configuration is managed through a special repository in your GitHub Organization: the `.fensak` repository.
This repository should contain your auto-approval rules and the mapping configuration for which rules apply to which
repos.

To make it easy to get started, we offer a template repository
([fensak-io/dotfensak-template](https://github.com/fensak-io/dotfensak-template)) that contains everything needed to
configure the `.fensak` repo. We recommend creating the `.fensak` repository in your Org by using the template repo. Refer to
the [official GitHub
documentation](https://docs.github.com/en/repositories/creating-and-managing-repositories/creating-a-repository-from-a-template)
for instructions on how to use a template repo.

> **NOTE**
>
> When creating your repo, be sure to name it `.fensak` instead of `dotfensak`!

Once the repository is created, feel free to take a look at what's included.
The template repository contains, amongst other things:
- A sample rule script that allows any changes that only modify the `README.md` file in the root of the repo.
- Test framework and setup for testing rules using [Deno](https://deno.com).
- A sample `fensak.yml` configuration file.
- A sample GitHub Actions workflow for CI of the rules scripts.

Try running the tests with `deno test` (note the required flags in the `README.md`!), or look at the sample rule file to
see what it looks like.

After looking around, you will want to at a minimum update the `fensak.yml` file. The config in the template repository points
Fensak at a fictional repository called `my-repo`. Unless you have a repository actually called `my-repo`, you will need to at least
update the `fensak.yml` configuration to get started. Be sure to update the reference to an actual repository that is in
your Org. Be sure to make the change on `main`, through a pull request!

> **IMPORTANT**
>
> Don't forget to enable branch protection on the `.fensak` repo!
>
> Treat your auto-approval rules like admin privileges. Access to modify the auto-approval rules means a user has
> arbitrary access to bypass protected branches in target repositories! You should guard this repository by following
> best practices:
> - Limit the teams that have write access to the repository.
> - Enable traditional protected branches. DO NOT enable Fensak on this repo!


## Create a test PR that passes and fails the sample rule

Once your `.fensak` repository is setup, you can start using Fensak! Fensak will automatically pull in the configuration
and rules from the `.fensak` repository once it starts seeing pull requests in your Org.

To see how Fensak monitors your pull requests, go to the repository that you configured in the `fensak.yml` file and
open a PR. We recommend creating two PRs, one with only a change to the `README.md` file and one that modifies another
file.

When you open a PR with a configured rule, Fensak will automatically create a check against the PR. The check contains
the results of running the rule against the change set, as well as an evaluation of the number of approvals on the PR.

![Screenshot of check run](/imgs/getting-started/fensak-check-run.png)

You should see the check pass on the PR containing only the change to the `README.md` file, while the check should fail
on the other PR since it will not have any reviews.

Click through to the details to see more information about the check. Fensak will report information like the reason for
a particular result, as well as any runtime console logs that are reported from the rules.

Here is an example of what it looks like on the check where it was auto approved:

![Screenshot of check details for a successful run](/imgs/getting-started/fensak-check-passed.png)

And here is an example of what a failed check looks like:

![Screenshot of check details for a failed run](/imgs/getting-started/fensak-check-failed.png)

On the failed PR, ask a coworker to submit an approval. A new Fensak check should be automatically triggered, and this
time the check should pass.

Note that at this point these checks are purely informational. To actually enforce protected branches, you also need to
set up protected branch rules on the repository to take advantage of the Fensak status check to block PRs when it fails.
In the next section, we will guide you through setting up the rules on the monitored repos so that the checks are
enforced.


## Configure protected branch rules on the monitored repo

Fensak by itself does not implement protected branches. It still relies on the GitHub native protected branches to
actually enforce the rules. However, your protected branch rules can be minimal with Fensak as most of the rules are
pushed to the Fensak service.

To enforce the Fensak check, create a protected branch rule for your trunk branch (typically `main` or `master`). Refer
to [the official GitHub
documentation](https://docs.github.com/en/repositories/configuring-branches-and-merges-in-your-repository/managing-protected-branches)
for information on how to do that.

Here is an example of the minimum setup needed to protect your branch:

![Screenshot of minimal protected branch setup](/imgs/getting-started/minimal-protected-branch-setup.png)

In the minimal setup, the following rules are turned on:
- Require a pull request before merging
    - This rule ensures that all changes must go through a pull request. No one will be allowed to directly and manually
      push changes to the trunk branch from the command line.
    - Note that if you wish to enable Continuous Delivery, you will need to disable the GitHub native required reviewers
      setting, since Fensak does not make an explicit GitHub approval on the PR.

- Require status checks to pass before merging, with the Fensak status check being required.
    - This is the core of enforcing the Fensak rules. With this rule, PRs can only be merged if the Fensak check passes.

The following rules are not necessary for enforcing Fensak checks, but are also recommended for further protection:
- Do not allow bypassing the above settings
    - This ensures that admins can't bypass the protection rules without turning it off first. Since every change to the
      protected branch setting is logged, you can easily audit when someone bypasses these rules with this setting
      turned on.

- Restrict who can push to matching branches
    - Use this setting to restrict the users can merge PRs. Note that this will need to include your bot users who are
      opening the PRs if you wish to implement Continuous Delivery (see next section).

With these settings, your repository is now protected with Fensak, while allowing some trivial routine changes
automatically.

However, there is one more step missing to allow automated Continuous Delivery: enabling `auto-merge` on the PR.


## Enable auto-merge on the repo

With the protected branch settings and Fensak rules, you have a framework for allowing changes to go through without
review. However, the current setup is fairly limiting for Continuous Delivery since the bot that is creating the
auto-deploy commit will need to wait for Fensak before it can merge the PR.

To avoid this synchronization step, you can use [GitHub
auto-merge](https://docs.github.com/en/pull-requests/collaborating-with-pull-requests/incorporating-changes-from-a-pull-request/automatically-merging-a-pull-request).
With GitHub auto-merge, the bot can stage the PR to automatically merge at the moment all necessary checks for protected
branches pass. This means that it no longer needs to wait for Fensak, and the PR can automatically merge as soon as the
Fensak check passes.

To allow PRs to be auto-merged, you must first allow auto-merge in the repository settings. This should be under the
General repository settings, towards the bottom of the `Pull Requests` heading.

![Screenshot of auto-merge setting in repository settings](/imgs/getting-started/auto-merge-setting-screenshot.png)

To implement Continuous Delivery workflows in this model, update your config changing bot to do the following using the
GitHub APIs:

1. Make the change that should be auto-deployed to the infrastructure code.
1. Create a branch, commit the change, and open a PR against trunk containing the change.
1. Update the PR to auto-merge once checks pass.

And that's it! Fensak and GitHub should take care of the rest, provided there are no merge conflicts blocking the PR
from being merged.


## Where to go from here

Congratulations! You just configured your first auto-approve rule using Fensak and walked through the steps end-to-end
on how to use Fensak for protecting your branches with Continuous Delivery.

From here, you should update your Fensak config to unlink the repository from the sample rule (unless you want to
auto-deploy README updates), and start defining custom rules that meet your needs.

For an overview of how to write custom rules, refer to our [Writing rules scripts guide](/docs/writing-rules).

For an overview of other Fensak configuration options, refer to our [Config file reference](/docs/config-reference).

If you need help, have additional questions, or any feedback for the service in general, head over to our [GitHub
Discussions forum](https://github.com/orgs/fensak-io/discussions).
