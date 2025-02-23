---
slug: scm 
append_help_link: true
title: Adding self-hosted repositories 
description: "Integrate Semgrep into self-hosted and custom SCM tools such as GitHub Enterprise and GitLab Self Hosted."
hide_title: true
tags:
    - Semgrep Cloud Platform
    - Team & Enterprise Tier
---

import MoreHelp from "/src/components/MoreHelp"

<ul id="tag__badge-list">
{
Object.entries(frontMatter).filter(
    frontmatter => frontmatter[0] === 'tags')[0].pop().map(
    (value) => <li class='tag__badge-item'>{value}</li> )
}
</ul>

# Integrating Semgrep Cloud Platform with self-hosted enterprise repositories 

This guide provides steps and prerequisites to fully enable all features of Semgrep Cloud Platform for **GitHub Enterprise Server** and **GitLab Self Managed** plans. 

:::note
This document covers the enablement of features for GitHub Enterprise **Server** plans. For users of GitHub Enterprise **Cloud** plans, see [Getting started with Semgrep Cloud Platform](/semgrep-app/getting-started-with-semgrep-app).
:::


:::info Prerequisites
You need the following permissions to integrate Semgrep into GHE Server or GLSM servers:

* Permission to create a **personal access token (PAT)** for the repository to scan with Semgrep. This PAT is used to enable Semgrep Cloud Platform to create pull request (PR) or merge request (MR) comments for findings. These comments provide a description of the issue detected by Semgrep and may offer possible solutions.
* Permission to add **CI/CD secrets** into your [GitHub](https://docs.github.com/en/actions/security-guides/encrypted-secrets) or [GitLab](https://docs.gitlab.com/ee/ci/secrets/) environments.
:::

## Table of required scopes for PATs

Semgrep Cloud Platform requires PATs with assigned scopes. These scopes grant necessary permissions to the PAT and vary depending on the user's plan.

| GitHub Enterprise Server          | GitLab Self-Managed        |
|:---------------------------|:---------------------------|
| <ul><li>`public_repo`</li> <li>`repo:status`</li> <li>`user:email`</li> <li>`write:discussion`</li></ul> | `api` |


## Integrating Semgrep Cloud Platform with GitHub Enterprise or GitLab Self Managed 

Integrate Semgrep into these custom source code management (SCM) tools by following the steps below:

1. Sign in to [Semgrep Cloud Platform](https://semgrep.dev/login).
2. Click **Settings** > **Source code**.

<div class = "bordered">

![Screenshot of SCM configuration tab](/img/app-scm.png)

</div>

3. Select your source code provider.
4. For **GitHub Enterprise Server**, follow these steps:

    1. Create a PAT by following the steps outlined in this [guide to creating a PAT](https://docs.github.com/en/enterprise-server@3.1/authentication/keeping-your-account-and-data-secure/creating-a-personal-access-token). Ensure that the PAT is **[created with the required scopes](../scm/#table-of-required-scopes-for-pats)**.
    2. Enter the personal access token generated into the **Access token** field.
    3. Enter your GHE Server base URL into the **URL** field.
    4. Ensure that your SCM integration successfully detects repositories by setting up a CI job for any repository you want to scan:
        1. Commit a `semgrep.yml` configuration file into the `.github/workflows` folder. Refer to [Sample CI configurations](/docs/semgrep-ci/sample-ci-configs#github-actions) for a template you can copy and customize. 
        2. The CI job starts automatically to establish a connection with Semgrep Cloud Platform. Upon establishing a connection, your repository appears in **Semgrep Cloud Platform > [Projects](https://semgrep.dev/orgs/-/projects)** page.
       3. Repeat all steps under step (iv) to add more repositories into Semgrep Cloud Platform.
5. For **GitLab Self Managed**, follow these steps:
    1. Create a PAT by following the steps outlined in this [guide to creating a PAT](https://docs.gitlab.com/ee/user/profile/personal_access_tokens.html). Ensure that the PAT is **[created with the required scopes](../scm/#table-of-required-scopes-for-pats)**.
    2. Enter the personal access token generated into the **Access token** field.
    3. Enter your GLSM base URL into the **URL** field.
    4. Ensure that your SCM integration successfully detects repositories by setting up a CI job for any repository you want to scan:
        1. Create or edit your `.gitlab-ci.yml` configuration file to add Semgrep as part of your GitLab CI/CD pipeline. Refer to [Sample CI configurations](/docs/semgrep-ci/sample-ci-configs#gitlab-cicd) for a template you can copy and customize.
        2. Commit the updated `.gitlab-ci.yml` file.
        3. The CI job starts automatically to establish a connection with Semgrep Cloud Platform. Alternatively, if it does not start automatically, start the job from the GitLab CI/CD interface. Upon establishing a connection, your repository appears in **Semgrep Cloud Platform > [Projects](https://semgrep.dev/orgs/-/projects)** page.
       4. Repeat all steps under step (iv) to add more repositories into Semgrep Cloud Platform.

## Receiving PR or MR comments in your VPN or on-premise SCM

PR or MR comments are comments or suggestions made by Semgrep Cloud Platform in your GitHub or GitLab repository. These comments provide a description of the issue detected by Semgrep and may offer possible solutions. These comments are a means for security teams (or any team responsible for creating standards) to help their fellow developers write safe and standards-compliant code.

To enable this feature within self-hosted SCMs behind firewalls or VPNs (Virtual Private Networks), follow these steps:

 1. Add the IP address `52.34.175.113` to your VPN's allowlist. This IP address is **static and outbound**.
 2. Test that you are able to receive findings by manually triggering a scan through your CI provider.

:::tip
Receiving PR or MR comments may require additional steps depending on the custom configuration of your VPN or SCM (for example, if you use a static IP without a hostname). Reach out to Semgrep support through the [Semgrep Community Slack](https://go.semgrep.dev/slack) or send an email to [support@r2c.dev](mailto:support@r2c.dev) for any concerns.
:::

## Additional references
* [Semgrep's May 2022 updates: DeepSemgrep, New Playground, and Self Managed GitHub and GitLab support](https://r2c.dev/blog/2022/semgreps-may-2022-updates/)


<MoreHelp />
