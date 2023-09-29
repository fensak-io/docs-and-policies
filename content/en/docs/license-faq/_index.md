---
title: License FAQ
description: FAQ about the Fensak dual-license
no_list: true
weight: 50
---

This is a collection FAQs about the specific licensing choice of Fensak.

> **IMPORTANT**
>
> This document does **NOT** constitute legal advice. Always consult a lawyer when dealing with legal concerns.
> The primary purpose of this document is to provide insight into the spirit of the license choices made at Fensak,
> which oftentimes is more important in understanding the intent behind our choices.


### What is the license for Fensak?

`SPDX-License-Identifier: BUSL-1.1 OR AGPL-3.0-or-later`

Fensak is dual-licensed under the
[Business Source License 1.1](https://mariadb.com/bsl-faq-adopting/) (with no
Additional Use Grant) and [AGPL 3.0](https://www.gnu.org/licenses/agpl-3.0.en.html) (or any later version). Refer to the
corresponding LICENSE files for the full parameters of either license:

- [LICENSE.BUSL-1.1](https://github.com/fensak-io/fensak/blob/main/LICENSE.BUSL-1.1)
- [LICENSE.AGPL-3.0-or-later](https://github.com/fensak-io/fensak/blob/main/LICENSE.AGPL-3.0-or-later)

Dual licensing means that you can use the code under the terms of **either** license. This means that you can choose to
license the code under one of the licenses, and do not need to comply with both liceses simultaneously.

For example, you can license the code under the AGPL 3.0 license to self host an instance of Fensak as an internal
production instance, provided that you haven't made any modifications to the code. This can be done even if the BUSL 1.1
license restricts you from running a production instance of Fensak.

Similarly, you can import the Fensak functions in test code under the BUSL 1.1 license and keep your code private,
despite the copyleft provisions of AGPL 3.0 that require you to Open Source it under the provisions of that license.

In this way, you can choose to use whatever license fits your needs for your use case.


### Why is Fensak dual-licensed? Isn't one enough?

Software licensing is becoming an increasingly complex decision to make. There are a plethora of Open Source Licenses
to choose from, with an ever growing list if you also include the so-called "Source Available" licenses like the
[Business Source License 1.1](https://mariadb.com/bsl11/). With such complexity, we understand that it can be
frustrating as a user to have to deal with multiple licenses on a project.

Nevertheless we were compelled to license Fensak under a dual license and believe it to offer a superior experience for
end users than the alternatives (just the AGPL 3.0 or just the BUSL 1.1 license).

The dual license comes from a desire to protect the business interests of Fensak, while providing as much freedom to
users as possible. As such, we ruled out all the permissive licenses (like BSD and MIT) early on since they give users
too much freedom to use the code to spin off competitors. On the other hand, "Source Available" licenses are too free
form and restrictive to users which can lead to widespread confusion, as evidenced by the recent transition of licenses
from an Open Source license to a Source Available license for HashiCorp tools.

As such, originally we were eyeing a single [AGPL 3.0](https://www.gnu.org/licenses/agpl-3.0.en.html) license for
Fensak. The copyleft provisions provide enough protections for business interests while still offering the software
as FOSS.

However, the copyleft provisions turned out to be problematic for a specific use case of the Fensak rules engine:
unit testing and development.

Given that we are using a non-standard JavaScript runtime, we wanted to offer the same functions we use for executing
the user rules directly to users for testing and development purposes. Under the AGPL, this would be problematic as now
the user would have to make their rules, which may contain proprietary code, available publicly. A solution would have
been to offer a test binary to test rules. This binary can be offered in a way such that it won't be linked into the
user defined rules code, but such integrations would be unergonomic and difficult to manage.

Hence, to solve this, we decided to offer Fensak under a secondary license that targets this specific use case of
testing and development. And we found the BUSL 1.1 license to be best suited for this purpose, since it naturally has
restrictions on production usage (as the last thing we want is a competitor using our rules engine directly in their
products).


### What can I do under the AGPL 3.0 license?

We find the explanation in the post [Open Source Software License 101: The AGPL
License](https://fossa.com/blog/open-source-software-licenses-101-agpl-license/) by the team behind
[FOSSA](https://fossa.com/) to be a good explanation and overview of the license. If you have a paid Medium
subscription, the post [Understanding the AGPL: the most misunderstood
license](https://medium.com/swlh/understanding-the-agpl-the-most-misunderstood-license-86fd1fe91275) is also an
excellent post on the AGPL.

In general, the following is true about the AGPL:

- If you are using Fensak **as a service**, then there is nothing to do as the copyleft provisions does not cross the
  network boundary. That is, calling Fensak over a network does **not** constitute generating a derivative work.
- If you are using the Fensak software **unmodified** (e.g. running a self-hosted copy), then there is nothing to do as
  long as you are truly running an unmodified version of Fensak and you point your users to the `fensak-io/fensak`
  repository.
- If you are using the Fensak software **modified** but **only for internal purposes** (the instance is not publicly
  available), then there is nothing to do as presumably your internal team already has access to the code.
- If you are using the Fensak software **modified** and it is **made available publicly**, then you must make the
  source code of the modified software available under a compatible license (which is almost always AGPL 3.0).
- If you are using Fensak **as a library** but **only for internal purposes** (that is, the combined work is not made
  available outside your Organization), then there is nothing to do as presumably your internal team already has access to the code.
- If you are using Fensak **as a library** and the combined work is accessible over a network (that is, the library is
  embedded in a service that is made externally available), then the **the whole service is a derivative work** and you
  must make it available under a compatible license.

Note that although technically using the test code in `fensak-io/fensak` to test your rules could be considered
"internal purposes," there may be interpretations where the rules may be considered to be joined with your proprietary
code when it is being evaluated on your pull requests. While Fensak would **never** exercise such frivolous
interpretations, it may pass in legal review by other forks of Fensak and thus we recommend always using the BUSL 1.1
license when importing Fensak as a library for testing your rules.


### What can I do under the BUSL 1.1 license?

In general, the core of the BUSL 1.1 license only allows usage of the software for testing and developement purposes.
While the BUSL 1.1 license is fairly standard, it leaves a lot of parameters for customization by the end software
product. This can leave two flavors of the BUSL 1.1 license with wildly different provisions on what you can do and
can't do. This is why it's important to always read every specific BUSL 1.1 license implementation, and in particular
the customizable parameters.

The main customizable parameters of the license are:

- The "Additional Use Grant," which defines extra provisions that allow limited or full production usage of the
  software.
- The "Change Date," which is when the software is available under an alternative license. This can never be more than 4
  years after the initial availability of the software.
- The "Change License," which is what license the software becomes available under after the Change Date.

The most important parameter is the "Additional Use Grant" which dictates what production usage is made available under
the license. This is also where every product implementation is different. For example, MariaDB, the first software
where the BUSL license was put in use, employs a node count based use grant (e.g.,
[MaxScale](https://mariadb.com/projects-using-bsl-11/) allows production use when the cluster is less than 3 servers).
On the other hand, [HashiCorp](https://www.hashicorp.com/bsl) restricts usage to non-competitors of HashiCorp.

In the case of Fensak, we offer no "Additional Use Grant" under the BUSL 1.1 license. You can only license Fensak under
the BUSL for development and testing purposes. If you want to use it for production purposes, either use it under the
terms of the AGPL 3.0 license, or access Fensak as a service through our [hosted instance](https://fensak.io).


### Which license should I use Fensak under?

We recommend licensing Fensak under the AGPL 3.0 license for situations where you want to run an unmodified self-hosted
version of Fensak, or if you were already intending on releasing your combined software under a compatible copyleft
license.

On the other hand, we recommend licensing Fensak under the BUSL 1.1 license for development, testing, and evaluation.
The BUSL gives you a no-strings attached way to use the Fensak code for non-production use cases, unlike the copyleft
provisions of the AGPL 3.0 license.
