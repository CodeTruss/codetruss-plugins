# CodeTruss for Claude Code

CodeTruss is the deterministic first-pass verification gate for AI-written code.
This plugin teaches Claude Code to operate the separately installed free
CodeTruss CLI as that gate: bind the task to an approved file boundary, run the
repository's own verification commands, and read the signed receipt the CLI
writes for every change.

Install:

```text
/plugin marketplace add DeliriumPulse/codetruss-plugins
/plugin install codetruss@codetruss
```

Then ask Claude to `Set up CodeTruss for this repository`.

Prerequisites:

- Git
- Node.js 20.9 or newer
- CodeTruss CLI v0.2.30 or newer from <https://codetruss.com/cli>

Skill instructions are verified against the shipped CLI v0.2.30.

The plugin contains no analyzer, bundled hook, MCP server, background service,
or upload path. It delegates hook installation to the tested CLI after developer
confirmation. Deterministic checks stay local: the 13 registry analyzers, scope
classification, secret detection on changed files, and the repository's own
verification commands. Security static analysis and the cross-file symbol graph
are hosted and run only for an explicitly requested full-codebase audit, so a
local receipt never contains injection or taint analysis and states that in its
own "What did not run" section. Provider-backed review, authentication, and
receipt sync require separate explicit developer actions.

Troubleshooting:

- Run `codetruss --version`; install or upgrade from the CLI page when it is
  missing or older than v0.2.30.
- Run `codetruss setup` for the guided local policy, verification-fingerprint,
  and hook flow. Do not replace it with hand-edited setup steps.
- Run `codetruss hooks status claude` and `codetruss hooks doctor claude`
  before changing or reinstalling Claude settings.
- Run `codetruss report latest` to read the newest receipt and
  `codetruss verify latest` to re-check its signature offline.
- Exit 1 means `REVIEW_REQUIRED`, exit 2 means `FAILED`, and both still produce
  a receipt. Exit 3 is a usage or environment failure.
- Report wrapper problems at <https://github.com/DeliriumPulse/codetruss-plugins/issues>
  and CLI/security problems at <https://github.com/DeliriumPulse/codetruss-cli/issues>.
- Follow <https://codetruss.com/security> for private vulnerability reporting
  and the current product security boundary.

Measured behaviour on public repositories is published at
<https://codetruss.com/benchmark>.

The wrapper files in this package are MIT licensed. The separately installed
CLI is source-visible and free to use under the CodeTruss CLI Proprietary
License and CodeTruss Terms of Service.
