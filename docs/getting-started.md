---
slug: getting-started
append_help_link: true
description: "Install Semgrep, run Semgrep locally, and learn about the benefits of running Semgrep in CI (continuous integration)."
title: Semgrep OSS Engine
hide_title: true
---

import MoreHelp from "/src/components/MoreHelp"
import Tabs from '@theme/Tabs';
import TabItem from '@theme/TabItem';

# Getting started with Semgrep OSS Engine

The Semgrep OSS Engine is the foundation of Semgrep. Detect bugs, style violations, security issues, and more by scanning your code locally using [community-contributed rules](https://semgrep.dev/explore) as well as your own custom rules.

## Installing and running Semgrep locally

Install and run [Semgrep CLI](https://github.com/returntocorp/semgrep/) to scan your code locally using Semgrep OSS Engine. Semgrep CLI runs offline on uncompiled code. **No code leaves your computer**.

:::info Prerequisite
Semgrep CLI installation requires Python 3.7 or later.
:::

1. Install Semgrep CLI. Use one of the following options depending on your system and preference:
    <Tabs
        defaultValue="macOS"
        values={[
        {label: 'macOS', value: 'macOS'},
        {label: 'Linux', value: 'Linux'},
        {label: 'Windows Subsystem for Linux (WSL)', value: 'Windows Subsystem for Linux (WSL)'},
        {label: 'Docker', value: 'Docker'},
        ]}
    >

    <TabItem value='macOS'>

    ```bash
    brew install semgrep
    ```

    Alternatively:

    ```bash
    python3 -m pip install semgrep
    ```

    </TabItem>

    <TabItem value='Linux'>

    ```bash
    python3 -m pip install semgrep
    ```

    </TabItem>

    <TabItem value='Windows Subsystem for Linux (WSL)'>

    ```bash
    python3 -m pip install semgrep
    ```

    </TabItem>

    <TabItem value='Docker'>

    ```bash
    docker run --rm -v "${PWD}:/src" returntocorp/semgrep semgrep --config=auto
    ```

    </TabItem>

    </Tabs>


2. Confirm installation by the following command:
    ```sh
    semgrep --version
    ```
3. Run recommended Semgrep Registry rules:
    <pre class="language-bash"><code>semgrep --config=auto <span className="placeholder">PATH/TO/SRC</span></code></pre>
    Substitute the optional placeholder <code><span className="placeholder">PATH/TO/SRC</span></code> with the path to your source code.

:::note
By default, when Semgrep Registry is used, Semgrep collects [usage metrics](./metrics.md).
:::

### Next steps

By completing this guide, you are now familiar with a simple use of Semgrep. Here are some additional resources to follow:

- Follow tutorials on [Learn Semgrep](https://semgrep.dev/learn/) to learn about Semgrep interactively.
- See [Running rules](./running-rules.md) to try out and understand more about Semgrep rules.
- See [CLI Reference](./cli-reference.md) for command line options and exit codes.
- Explore the Semgrep [Rules Registry](https://semgrep.dev/explore) to add rules to your project or [writing a rule](./writing-rules/overview.md).

## Testing Semgrep on vulnerable repositories

The following community projects are designed to test code scanners and teach security concepts. Try cloning and scanning them with Semgrep.

<details><summary>Expand for sample projects! 🎉</summary>
<p>

```sh
# juice-shop, a vulnerable Node.js + Express app:
git clone https://github.com/bkimminich/juice-shop
cd juice-shop
semgrep --config=auto

# Or if you don't have Semgrep installed, replace the semgrep command with:
docker run --rm -v "$(pwd)/juice-shop:/src" returntocorp/semgrep semgrep --config p/security-audit /src

# Try railsgoat, a vulnerable Ruby on Rails app:
git clone https://github.com/OWASP/railsgoat
cd railsgoat
semgrep --config=auto

# govwa, a vulnerable Go app:
git clone https://github.com/0c34/govwa
cd govwa
semgrep --config=auto 

# Vulnerable-Flask-App, vulnerable Python + Flask:
git clone https://github.com/we45/Vulnerable-Flask-App
cd Vulnerable-Flask-App
semgrep --config=auto 

# WebGoat, a vulnerable Java + Spring app:
git clone https://github.com/WebGoat/WebGoat
cd WebGoat
semgrep --config=auto 
```

</p>
</details>

## Run Semgrep continuously

Semgrep is at its best when used to continuously scan code. Check out [Semgrep in CI](semgrep-ci/overview.md/) to learn how to get results where you already work: GitHub, GitLab, Slack, Jira, and more. To get results even earlier in the development process, such as in a Git pre-commit hook or VS Code, check the available [Semgrep extensions](./extensions.md).

Check out [Semgrep Cloud Platform](https://semgrep.dev/manage) (SCP) to integrate Semgrep scans into your CI environment with PR or MR comments, monitor progress, host private rules (Team and Enterprise tiers), and much more! 

## Logging into Semgrep Cloud Platform

Logging into SCP from your CLI enables you to:

* Send findings from your local scans to SCP for findings triage.
* Quickly configure local scans to run either rules from your Rule board or a different set of rules and rulesets. 
* For Team or Enterprise users: scan code using Pro rules from the CLI.

To log in to SCP:

1. Create an account by clicking the link: [Sign in to Semgrep Cloud Platform](https://semgrep.dev/login).
2. In your command line, enter `semgrep login`.
3. Click the link provided in your terminal and follow the instructions.

## Updating Semgrep

We [release new Semgrep versions](https://github.com/returntocorp/semgrep/releases) often! See [Updating](./upgrading.md) for more details.

<MoreHelp />
