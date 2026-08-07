# Plugin submission answers

Paste-ready answers for the two submissions that a human has to file. Both
target audiences forbid or discourage agent-filed submissions, so an agent
prepared this file and a person files the forms. Budget about 10 minutes total.

Everything below is already true of the repository at HEAD. Nothing here needs
to be built first.

## Preflight, already done

- `claude plugin validate . --strict` passes on the marketplace manifest.
- `claude plugin validate ./plugins/codetruss-claude --strict` passes on the
  plugin manifest.
- `npm test` passes.
- The self-hosted marketplace is live and installable today:
  `/plugin marketplace add DeliriumPulse/codetruss-plugins` then
  `/plugin install codetruss@codetruss`. Verified end to end against the public
  repository on 2026-08-06 with Claude Code 2.1.218.
- Installed component inventory, as Claude Code reports it: Skills 1, Agents 0,
  Hooks 0, MCP servers 0, LSP servers 0. Always-on cost about 108 tokens.

## 1. Community marketplace, Console form

Form: <https://platform.claude.com/plugins/submit>

Use the Console form, not the claude.ai form. The claude.ai form requires a Team
or Enterprise organization; the Console form works for individual authors.

The form is behind a login, so the exact field labels could not be captured
here. The answer bank below covers what a plugin submission asks for. Match each
value to the closest field and skip what is not asked.

| Topic | Value to paste |
|---|---|
| Repository | `https://github.com/DeliriumPulse/codetruss-plugins` |
| Marketplace name | `codetruss` |
| Plugin name | `codetruss` |
| Plugin path in repo | `plugins/codetruss-claude` |
| Version | `0.1.6` |
| Category | `development` |
| License | MIT for the plugin wrappers |
| Homepage | `https://codetruss.com/cli` |
| Author | Zack Whitson, `zack@codetruss.com` |
| Issue tracker | `https://github.com/DeliriumPulse/codetruss-plugins/issues` |
| Security contact | `zack@codetruss.com`, policy in `SECURITY.md` |

Short description, one line:

> Bind each agent task to an approved file boundary, run the repository's own
> checks, and read the signed receipt. Requires the separately installed free
> CodeTruss CLI.

Long description, if the form has a larger field:

> CodeTruss is the deterministic first-pass verification gate for AI-written
> code. This plugin adds one skill that teaches Claude Code to operate the
> separately installed CodeTruss CLI: propose a narrow allow and deny boundary
> for the task, run the repository's own verification commands, and interpret
> the signed receipt the CLI writes for the session. Analysis is deterministic
> and local. The 13 registry analyzers, scope classification, secret detection
> on changed files, and the verification commands all run on the developer's
> machine with no account and no network. Security static analysis and the
> cross-file symbol graph are hosted and run only for an explicitly requested
> full-codebase audit, so a local receipt never contains injection or taint
> analysis and states that in its own "What did not run" section. The plugin
> ships no analyzer, no bundled hook, no MCP server, and no upload path; hook
> installation is delegated to the CLI's own tested installer after the
> developer confirms it.

If the form asks what the plugin does that could concern a reviewer:

> The skill invokes a separately installed CLI with the agent's local
> permissions. It never installs software, authenticates, enables
> provider-backed review, or syncs a receipt without explicit developer
> confirmation. It writes only inside the developer's repository. The wrapper
> contains no executable code of its own.

## 2. awesome-claude-code

Form: the repository's "Recommend a Resource" issue form at
<https://github.com/hesreallyhim/awesome-claude-code/issues/new/choose>.
Do not open a pull request; the maintainer only accepts the form. The
CONTRIBUTING file states that coding agents must not file these, so this one has
to be filed by hand.

Eligibility check, already satisfied: the repository's first commit to the
default branch was on 2026-07-14, which is more than 14 days of active
development. Only one resource may be submitted at a time.

Field by field:

- **Title** (prefilled `[Resource]: <name of your resource>`):
  `[Resource]: CodeTruss`
- **Display Name**: `CodeTruss`
- **Category**: `Skills`
- **Link**: `https://github.com/DeliriumPulse/codetruss-plugins`
- **Author Name**: `Zack Whitson`
- **Author Link**: `https://github.com/DeliriumPulse`
- **Description** (10 to 500 characters, descriptive not promotional, do not
  address the reader):

> A skills-only plugin that drives the CodeTruss CLI as a deterministic
> first-pass gate on agent-written changes. It binds a session to an approved
> file boundary, runs the repository's own verification commands, and reads the
> signed receipt the CLI writes, which records what ran and what did not. The
> CLI is free, needs no account, and analyzes locally; the plugin wrappers are
> MIT licensed.

That last sentence is deliberate. The list's screening notes treat closed-source
resources that require signup or payment as blockers, so the description states
plainly that the plugin is MIT, the CLI is free, and no account is involved.

- **Checklist**: check the first five boxes after actually doing them. Leave the
  sixth box unchecked. It is a trap that reads "Do not check the following box"
  and checking it flags the submission as unread.

Variant if you would rather list the CLI, which is what the acquisition plan
originally named: change **Link** to
`https://github.com/DeliriumPulse/codetruss-cli`, change **Display Name** to
`CodeTruss Boundary`, and replace "A skills-only plugin that drives the
CodeTruss CLI" with "A local CLI". Everything else stands. The plugin
repository is the recommended entry because the list requires resources specific
to Claude Code and the plugin repository is both Claude Code specific and fully
MIT licensed.

## Not submitted here, and why

The GitHub Marketplace listing, the MCP registry publish, and the
`claude-plugins-official` curation request are separate tracks with their own
prerequisites. The official marketplace has no application process; it is a
partner conversation, and the CLI hint protocol is the concrete ask to bring to
it.
