---
title: Getting started with BranchFuse
permalink: /getting-started
---

# Getting started with BranchFuse

BranchFuse runs Bitbucket Cloud Pipelines and GitHub Actions workflows for any branch from your JetBrains IDE, follows
them live and turns failures into clickable file:line links. This guide takes you from installing the plugin to your
first run in a few minutes.

## Before you start

You need:

- **A JetBrains IDE, version 2025.1 or newer,** with Git support: IntelliJ IDEA, PhpStorm, WebStorm, PyCharm, GoLand,
  Rider, CLion and others.
- **A project opened from a Git repository** whose remote is on **bitbucket.org** or **github.com**. Bitbucket
  Server/Data Center, GitHub Enterprise Server and other CI services aren't supported.
- **Something to run:**
  - Bitbucket: a repository with Pipelines enabled and a `bitbucket-pipelines.yml`. BranchFuse can run the branch
    pipeline and any `custom` pipeline.
  - GitHub: a workflow in `.github/workflows/` with a `workflow_dispatch` trigger. GitHub only lets you start a
    workflow this way if the workflow file is also on the repository's default branch.
- **Permission to create a token** for that repository (steps 4 and 5 explain which one).

## Step 1: Install BranchFuse

1. In your IDE, open **Settings** (**Preferences** on macOS) and go to **Plugins**.
2. Select the **Marketplace** tab and search for **BranchFuse**.
3. Click **Install**, then **Restart IDE** when asked.

## Step 2: Start your free trial

BranchFuse is a paid plugin with a **7-day free trial**, licensed through JetBrains Marketplace.

1. Open the **BranchFuse** tool window: click its icon in the right-hand tool window bar, or use
   **View | Tool Windows | BranchFuse**.
2. If it says **BranchFuse needs a licence**, click **Buy, activate or start the free trial…**.
3. In the IDE's licence dialog, start the trial, or activate your licence if you've already bought one.

The tool window updates by itself as soon as the trial or licence is active. If a licence ends later, your accounts
and settings are kept, and everything works again once a licence is active.

## Step 3: Open your project and the tool window

Open the project you want to run CI for, then open the **BranchFuse** tool window.

BranchFuse reads the project's Git remotes to find its repository. The first time, you'll see **Get started with
BranchFuse** with four steps:

1. **Repository found**: shows the repository it detected, for example `your-team/your-repo on GitHub`.
2. **Create a token and add it**
3. **Test the connection**
4. **Pick a pipeline and run it**

If BranchFuse can't find a repository, check that the project's Git remote points at bitbucket.org or github.com.
If the project has several remotes pointing at different repositories (for example a fork and its upstream), choose
the right one later in **Settings | Tools | BranchFuse | This project | Repository**.

Follow step 4 for GitHub or step 5 for Bitbucket, then continue with step 6.

## Step 4 (GitHub): Create a token

BranchFuse needs a **fine-grained personal access token** that can see your repository.

1. In the *Get started* panel, click **Create a pre-filled GitHub token**. GitHub opens with the permissions BranchFuse
   needs already filled in:
   - **Actions: Read and write** (to start, follow and stop runs)
   - **Contents: Read-only** (to read your workflow files)
   - **Metadata: Read-only** is added automatically.
2. Give the token a name and an expiration date.
3. Under **Repository access**, choose **Only select repositories** and pick the repositories you want to run.
4. Click **Generate token** and copy it. GitHub shows it only once.

You can also create one yourself at <https://github.com/settings/personal-access-tokens/new> with the permissions
above. A **classic** token works too, with the scopes `repo` and `workflow`.

**Organisations:** some organisations have to approve fine-grained tokens before they can access their repositories.
If the connection test fails with a permission error, ask an organisation owner to approve your token.

## Step 5 (Bitbucket Cloud): Create a token

BranchFuse needs an **Atlassian API token with scopes**.

1. In the *Get started* panel, click **Create an Atlassian API token**, or go to
   <https://id.atlassian.com/manage-profile/security/api-tokens>.
2. Choose **Create API token with scopes**, give it a name and an expiry date.
3. Select **Bitbucket** as the app.
4. Tick exactly these scopes:
   - `read:repository:bitbucket`
   - `read:pipeline:bitbucket`
   - `write:pipeline:bitbucket`
   - `read:user:bitbucket` (lets *Triggered by me* in History tell which runs you started)
5. Create the token and copy it. Atlassian shows it only once.

You'll also need the **email address of your Atlassian account**: Bitbucket uses it together with the API token.

**Alternative:** a **repository, project or workspace access token** also works, with the permissions `repository`
(read), `pipeline` (read) and `pipeline:write`. It needs no email, but you need admin rights on the repository,
project or workspace to create one. App passwords aren't supported.

## Step 6: Add the account and test it

1. In the *Get started* panel, click **Add Account and Test…**.
2. In the **Add Account** dialog, check the **Service** (GitHub or Bitbucket Cloud), then fill in:
   - **Name:** any name you'll recognise, for example *Work GitHub*.
   - **Authentication:** *Personal access token* for GitHub; *Atlassian API token* or *Repository / workspace access
     token* for Bitbucket.
   - **Atlassian email** (Bitbucket API token only): the email of your Atlassian account.
   - **Token:** paste the token you copied.
3. Click **OK**. BranchFuse tests the token against your repository and saves the account only if every check passes.

When the test passes, the *Get started* panel is replaced by the run form. If it fails, the message says what's
missing, usually a scope or the repository not being included in the token.

Your token is stored only in the IDE's password safe (your system keychain or KeePass). It's never written to
project or settings files, never logged, and sent only to `api.github.com` or `api.bitbucket.org`.

**Already have an account?** Click **Already have an account? Open BranchFuse settings**, choose it under **This
project | Account**, and click **Test Connection**. You can use one account for many projects.

## Step 7: Run your first pipeline or workflow

The run form shows the repository at the top, then:

1. **Branch:** your current branch comes first, then the branches you used recently. Below it, BranchFuse tells you
   which commit will run, for example *Will run 1a2b3c4 from origin/feature/login*. It warns you before running if:
   - the branch isn't pushed yet (offering **Push**),
   - you have commits that aren't pushed (the run would use the older remote version), or
   - the remote has commits you haven't fetched.
2. **Pipeline:** pick a Bitbucket pipeline (the branch pipeline or a custom one) or a GitHub workflow. Only pipelines
   and workflows that exist on that branch are listed.
3. **Inputs or variables:** fill in the form generated from the pipeline:
   - GitHub workflow `inputs`: choices appear as lists, booleans as true/false, everything else as a text field.
   - Bitbucket custom pipeline `variables`: tick **Secured** for secrets, so Bitbucket masks them. BranchFuse never
     stores secured values.
   - Required fields without a default must be filled in before **Run** is enabled.
4. Click **Run**. Pipelines that deploy (a Bitbucket `deployment:` or a GitHub job with an `environment:`) always ask
   you to confirm first.

## Step 8: Follow the run

- The **Steps** tab shows each Bitbucket step or GitHub job with its live status and duration. BranchFuse checks
  every few seconds and slows down for long runs.
- The **status bar** shows the latest run of your current branch, for example *#42 Running*. Click it to open the
  run.
- When the run finishes, a notification tells you how it ended. Click **Show in BranchFuse** to open it.
- The toolbar has **Stop Run…**, **Refresh Run** and **Open Run in Browser**.
- Runs started by your pushes from the IDE are followed automatically too. Turn this off with **Follow Runs from My
  Pushes** in the toolbar.

## Step 9: Fix failures

When a run fails, BranchFuse opens the **Failures** tab:

- Each failed test or error is listed with its reason. Expand one to see:
  - **Open *File*.php:35**: the line in your application code where it failed.
  - **Open test *FileTest*.php:50**: the line in the test.
  - **Show Step Log**: the step's log, at that failure.
- Bitbucket test reports (JUnit) are used when your pipeline produces them. Otherwise BranchFuse finds failures in the
  log, for PHPUnit, PHPStan, Psalm, Gradle, Maven, Kotlin, Java, Jest, Vitest, pytest, Go, TypeScript, ESLint, .NET
  and any `file:line`.
- **In the editor**, failing lines are highlighted with a red gutter icon. Hover over it to see why the line failed.
  Turn this on or off with **Show CI Failures in Editor** in the toolbar.
- The **Log** tab shows a step's log with secrets masked. Use **Filter lines** to search it, and click any
  `file:line` to open it.

If the run built a different commit than the one you have checked out, BranchFuse warns you that the line may have
moved.

## Step 10: Rerun and look back

- **Rerun** runs the shown run again on the same commit with the same inputs. On GitHub, **Rerun Failed Jobs** reruns
  only the failed jobs. Bitbucket can rerun only failed steps on its website, so BranchFuse opens the run page there.
- **Recent Runs** lists the runs you started or opened in the IDE.
- **History** lists the repository's runs, with filters for branch, state (*In progress*, *Succeeded*, *Failed*,
  *Stopped or skipped*) and pipeline. Star the pipelines you use most and tick **Starred only**, or tick **Triggered
  by me**.

## Optional: path mappings for Docker builds

BranchFuse maps the build folders of Bitbucket Pipelines and GitHub-hosted runners to your project automatically, and
matches other paths by the end of the path when only one project file fits. Most projects need no setup.

If your build runs in its own working folder, for example `/app` inside a Docker image, and a failure link opens the
wrong file or none, add a rule in **Settings | Tools | BranchFuse | Path mappings**:

| CI path | Local folder |
|---|---|
| `/app` | `.` (the Git root) or a folder relative to it |

## Troubleshooting

| Problem | What to do |
|---|---|
| *BranchFuse isn't connected for this project* | Check that the project's Git remote is on bitbucket.org or github.com, then use **Reload BranchFuse** in the toolbar. |
| *Connection Problem* when testing | Check the token's scopes or permissions (steps 4 and 5) and that it includes this repository. For a Bitbucket API token, check the Atlassian email. |
| A GitHub workflow isn't listed | It needs an `on: workflow_dispatch` trigger, and the workflow file must also be on the default branch. |
| A Bitbucket pipeline isn't listed | Check that `bitbucket-pipelines.yml` on that branch defines it as the branch pipeline or under `custom:`. |
| **Run** stays disabled | A required input or variable is empty. |
| *Branch … isn't on origin yet* | Push the branch first. BranchFuse never runs a different branch instead. |
| Failure links open the wrong file | Add a path mapping (see above). |
| Tokens disappear after restarting the IDE | Your IDE is set not to save passwords. Change it in **Settings \| Appearance & Behavior \| System Settings \| Passwords**. |

## Privacy

BranchFuse has no server and sends no telemetry. It talks only to `api.bitbucket.org` and `api.github.com`, with your
own token. See the [privacy policy](privacy) for details.

## Help

Questions or problems: email **ibrahimdavid08@gmail.com**.
