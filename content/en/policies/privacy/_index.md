---
title: Privacy Policy
linkTitle: Privacy Policy
type: "docs"
no_list: true
---

*Last updated: Oct 13th, 2023*

The privacy of your data — and it is your data, not ours! — is a big deal to us. In this policy, we lay out:

* what data we collect and why
* how your data is handled
* and your rights with respect to your data.

We promise we will not sell your data. Never have. Never will.

We may update this policy as needed to comply with relevant regulations and reflect any new practices. You can view a
history of the changes to our policies [on
GitHub](https://github.com/fensak-io/docs-and-policies/commits/main/content/en/policies/privacy/_index.md). Whenever we
make a significant change to our policies, we will refresh the date at the top of this page and take any other
appropriate steps to notify users.


## What We Collect and Why

Our guiding principle is to collect only what we need. Here’s what that means in practice:

### Identity & Access

When you sign up for Fensak, we get access to your GitHub profile which may include details like your name, email
address, and a company name. We only store the GitHub Organization slug on our servers, while other relevant information
is only pulled from GitHub as needed. This information allows us to identify customers on the platform so that we can
provide the intended services.

Rest assured, we will never sell your personal information to third parties, nor will we use your name or company
in marketing materials without your permission.

### Billing Information

When you join Fensak, we'll ask for your payment details and billing address. Your credit card information
goes straight to our Merchant of Record ([Paddle](https://paddle.com)), not passing through Fensak servers. Our Merchant
of Record saves the transaction and billing details to help with account history, invoicing, and billing support. We
also save a record of the transaction identifier on our servers, to help with subscription management.

Our Merchant of Record also keeps your billing address to charge you for our service, figure out any sales tax, send
invoices, and spot any fraudulent transactions.

For more information on how our Merchant of Record uses your information, refer to [their Privacy
Policy](https://www.paddle.com/legal/gdpr).

### Product Interactions

We have access to all events related to Pull Requests in your Organization through the installed GitHub app. These pull
request event data allows us to know which change sets need to be reviewed, and to pass the change set information to
the rules scripts to provide the intended services. This data is used in-memory and discarded at the end of the
processing routine. We do not store any information about the pull request content on our servers.

We may log metadata about the pull request event for debugging purposes. The logs may contain information such as your
GitHub Organization slug, the source repository name, or the specific PR number. This information is only used in the
event of an error on our servers, or to help with a support request.

### Configuration data

We store the contents of the configuration file and compiled, minified rule scripts in the `.fensak` repository. This
allows us to cache the configuration so that we can offer a superior experience and stay within the limits of our
service providers. This data is deleted when you cancel and uninstall the GitHub app.

### Geolocation Data

We log the IP address you use when accessing our websites, such as [https://fensak.io](https://fensak.io),
[https://dash.fensak.io](https://dash.fensak.io), and [https://docs.fensak.io](https://docs.fensak.io) for security and
fraud prevention purposes.

### Website Analytics

We use [Plausible Analytics](https://plausible.io/) to track overall trends in the usage of our website. Plausible
Analytics collects only aggregated information, which does not allow us to identify any visitor to our website. For more
information, please visit the [Plausible Analytics Data Policy](https://plausible.io/privacy).

### Anti-Bot Assessments

We proxy our service through [Cloudflare](https://www.cloudflare.com/) to mitigate brute force and DDoS attacks. We have
a legitimate interest in protecting our apps and the broader Internet community from credential stuffing
attacks and spam. When you access our websites, Cloudflare evaluates various information (e.g., IP address, how long the
visitor has been on the app, mouse movements) to try to detect if the activity is from an automated program instead of a
human. We retain these data via our subprocessor indefinitely for use in spam mitigation.

For more information, please visit the [How Cloudflare works
page](https://developers.cloudflare.com/fundamentals/get-started/concepts/how-cloudflare-works/) and the [Cloudflare
Privacy Policy](https://www.cloudflare.com/privacypolicy/).

### Cookies

We use some persistent third-party cookies to store certain preferences, make it easier for you to browse our websites,
and perform A/B testing.

A cookie is a piece of text stored by your browser. It may help remember login information and site preferences. It
might also collect information such as your browser type, operating system, web pages visited, duration of visit,
content viewed, and other click-stream data. You can adjust cookie retention settings and accept or block individual
cookies in your browser settings, although our apps won’t work and other aspects of our service may not function
properly if you turn cookies off.

Note that currently all cookies on our websites (listed below) are required for it to function properly. Rejecting
cookies in our consent banner will only reject the optional cookies, including cookies that we may introduce in the
future that will not be required for the site to function (e.g., for personalization or A/B testing).

#### Third Party Cookies

Fensak uses the following third-party Cookies:

| Cookie Name | Type     | Expiry           | Use                                                                                                                                                                                                                                                                     |
| ---         | ---      | ---              | ---                                                                                                                                                                                                                                                                     |
| Cloudflare  | Required | at most 24 hours | Bot management and session affinity for global cache. Refer to the [Cloudflare Privacy Policy](https://www.cloudflare.com/privacypolicy/) for more details on the cookies and their use.                                                                                |
| CookieYes   | Required | 1 year           | Tracking consent information for our Cookie Policy. Refer to the [CookieYes Cookie Policy](https://www.cookieyes.com/cookie-policy) for more details on the cookies and their use.                                                                                      |


### Voluntary Correspondence

When you contact Fensak for help or questions, we keep the correspondence, including your email address,
to better assist you in the future. We also store information you voluntarily provide, such as survey responses or
recordings of customer interviews (with your express consent).

## When We Access or Share Your Information

**To provide products or services you’ve requested**. We may use third-party subprocessors to help run our applications
and provide the Services to you. The following is a list of third-party subprocessors we use:
* [Cloudflare](https://www.cloudflare.com/privacypolicy/). Cloud services provider.
* [Deno Deploy](https://docs.deno.com/deploy/manual/privacy-policy). Cloud services provider.
* [CookieYes](https://www.cookieyes.com/privacy-policy/). Cookie consent service provider.
* [HubSpot](https://www.hubspot.com/data-privacy/gdpr). Customer sales and ticketing service.
* [GitHub](https://docs.github.com/en/site-policy/privacy-policies/github-data-protection-agreement). Version control
  software, help forum, and end user platform.
* [Carrd](https://carrd.co/docs/general/privacy). Landing page provider.
* [Paddle](https://www.paddle.com/legal/gdpr). Merchant of record.

No Fensak human looks at your data except with your express permission for limited purposes, such as an
error that stops an automated process from working and requires manual intervention to fix. These are rare cases,
after which, we look for root cause solutions to avoid them recurring to the extent possible. We may also access
your data as required for legal compliance under applicable laws and regulations (see “When required under applicable law” below).

**To help you troubleshoot or squash a software bug, with your permission.** If at any point we need to access your
content to help you with a support case, we will ask for your consent before proceeding.

**To investigate, prevent, or take action regarding restricted uses.** Accessing your account when investigating
potential abuse is a measure of last resort. We want to protect the privacy and safety of both our customers and the
people reporting issues to us, and we do our best to balance those responsibilities throughout the process. If we
discover you are using our products for a restricted purpose, we will take any necessary action, including notifying appropriate authorities where warranted.

**When required under applicable law.** Fensak, LLC is a U.S. company and all data infrastructure are located in the U.S.

* **Requests for user data.** Our policy is to not respond to government requests for user data unless we are compelled
  by legal process or in limited circumstances in the event of an emergency request. However, if U.S. law enforcement
  authorities have the necessary warrant, criminal subpoena, or court order requiring us to share data, we must comply.
  Likewise, we will only respond to requests from government authorities outside the U.S. if compelled by the U.S.
  government through procedures outlined in a mutual legal assistance treaty or agreement. It is Fensak’s policy to
  notify affected users before we share data unless we are legally prohibited from doing so, and except in some
  emergency cases.
* **Preservation requests.** Similarly, Fensak’s policy is to comply with requests to preserve data only if
  compelled by the U.S. Federal Stored Communications Act, 18 U.S.C. Section 2703(f), or by a properly served U.S.
  subpoena for civil matters. We do not share preserved data unless required by law or compelled by a court order that
  we choose not to appeal. Furthermore, unless we receive a proper warrant, court order, or subpoena before the required
  preservation period expires, we will destroy any preserved copies of customer data at the end of the preservation
  period.
* **Audits.** If we are audited by a tax authority, we may be required to share billing-related information. If that
  happens, we will share only the minimum needed, such as billing addresses and tax exemption information.

Finally, if Fensak, LLC is acquired by or merges with another company we’ll notify you well before any of your
personal information is transferred or becomes subject to a different privacy policy.

## Your Rights with Respect to Your Information

At Fensak, we strive to apply the same data rights to all customers, regardless of their location. Some of these
rights include:
* **Right to Know.** You have the right to know what personal information is collected, used, shared or sold. We outline
  both the categories and specific bits of data we collect, as well as how they are used, in this privacy policy.
* **Right of Access.** This includes your right to access the personal information we gather about you, and your right
  to obtain information about the sharing, storage, security and processing of that information.
* **Right to Correction.** You have the right to request correction of your personal information.
* **Right to Erasure / “To Be Forgotten”.** This is your right to request, subject to certain limitations under
  applicable law, that your personal information be erased from our possession and, by extension, from all of our
  service providers. Fulfillment of some data deletion requests may prevent you from using Fensak services because
  our applications may then no longer work. In such cases, a data deletion request may result in closing your account.
* **Right to Complain.** You have the right to make a complaint regarding our handling of your personal information with
  the appropriate supervisory authority.
* **Right to Restrict Processing.** This is your right to request restriction of how and why your personal information
  is used or processed, including opting out of sale of personal information. (Again: we never have and never will sell
  your personal data.)
* **Right to Object.** You have the right, in certain situations, to object to how or why your personal information is
  processed.
* **Right to Portability.** You have the right to receive the personal information we have about you and the right to
  transmit it to another party.
* **Right to not Be Subject to Automated Decision-Making.** You have the right to object to and prevent any decision
  that could have a legal or similarly significant effect on you from being made solely based on automated processes.
  This right is limited if the decision is necessary for performance of any contract between you and us, is allowed by
  applicable law, or is based on your explicit consent.
* **Right to Non-Discrimination.** We do not and will not charge you a different amount to use our products, offer you
  different discounts, or give you a lower level of customer service because you have exercised your data privacy
  rights. However, the exercise of certain rights may, by virtue of your exercising those rights, prevent you from using
  our Services.

Many of these rights can be exercised by signing in and updating your account information.

If you have questions about exercising these rights or need assistance, please contact us at
[support@fenak.io](mailto:support@fensak.io).

If you are in the EU or UK, you can contact your data protection authority to file a complaint or learn more about local
privacy laws.

## How We Secure Your Data

All data is encrypted via [SSL/TLS](https://en.wikipedia.org/wiki/Transport_Layer_Security) when transmitted to and from
GitHub to and from our servers. Our application databases are encrypted at rest. All data are written to multiple disks
instantly, backed up daily, and stored in multiple locations.

## Location of Site and Data

Our products and other web properties are operated in the United States. If you are located in the European Union, UK,
or elsewhere outside of the United States, **please be aware that any information you provide to us will be transferred
to and stored in the United States**. By using our websites or Services and/or providing us with your personal
information, you consent to this transfer.

## Questions

Have any questions, comments, or concerns about this privacy policy, your data, or your rights with respect to your
information? Please get in touch by emailing us at [support@fensak.io](mailto:support@fensak.io) and we’ll be happy to help!

*These policies were adapted from the [Basecamp open-source policies](https://github.com/basecamp/policies) / [CC BY 4.0](https://creativecommons.org/licenses/by/4.0/).*
