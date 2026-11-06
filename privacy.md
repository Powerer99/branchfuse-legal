---
title: BranchFuse privacy policy
permalink: /privacy
---

# BranchFuse privacy policy

Last updated: 6 November 2026

BranchFuse is a plugin for JetBrains IDEs, made by David Gorgi Ibrahim ("we"). This policy explains what happens to your
data when you use it. In short: **BranchFuse has no server. We don't collect, receive or store any of your data.**

## What BranchFuse does with your data

- **Credentials.** The Bitbucket or GitHub token you enter is stored only in your IDE's password safe (your system
  keychain, KeePass, or memory, as you choose in the IDE). It's sent only to the service it's for
  (`api.bitbucket.org` or `api.github.com`) to authenticate your requests. It never appears in settings files, logs or
  error messages.
- **Your repositories and pipelines.** BranchFuse reads branch, pipeline, workflow, run, step, log and test report
  information from Bitbucket Cloud or GitHub to show it in your IDE. It starts or stops a run only when you click to
  do so. It talks only to `api.bitbucket.org` (and Bitbucket's log storage) and to `api.github.com` (and GitHub's log
  storage), and never sends your data anywhere else.
- **Pipeline variables and workflow inputs.** Values you enter when starting a run are sent to Bitbucket or GitHub in
  that request. Secured Bitbucket values are never stored and are masked wherever BranchFuse shows text. GitHub shows
  workflow inputs on the run's page, so don't enter secrets as inputs.
- **Settings.** Your account name, the account's email address and your project settings (chosen account, repository,
  path mappings, recent branches and runs) are stored on your computer in the IDE's configuration and project files.
- **Your own use.** Which BranchFuse features you have tried (for the trial note) and the last version whose *What's new*
  you saw are stored on your computer only. They are never sent anywhere.
- **Logs and test results** are kept in memory while the IDE is open and are never written to disk by BranchFuse.

## What we don't do

- We don't run any server for BranchFuse, and BranchFuse sends nothing to us.
- No telemetry, analytics, crash reporting or tracking.
- We don't sell or share data. We never have it.

## Third parties

- **Atlassian Bitbucket Cloud** receives your requests, under Atlassian's own privacy policy.
- **GitHub** receives your requests when you use a GitHub account, under GitHub's own privacy statement.
- **JetBrains** handles plugin distribution, payment and licensing through JetBrains Marketplace, under the JetBrains
  privacy policy. BranchFuse checks your licence only through the IDE's built-in licensing; it makes no licensing
  requests of its own.

## Your choices

Remove an account in *Settings | Tools | BranchFuse* to delete its token from the password safe. Uninstalling the
plugin stops all requests. You can revoke a token at any time in your Atlassian or GitHub account.

## Changes

If this policy changes, the new version is published at <https://powerer99.github.io/branchfuse-legal/privacy>
with a new date.

## Contact

David Gorgi Ibrahim — ibrahimdavid08@gmail.com
