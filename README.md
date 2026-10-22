# Esper Brain

> AI agents and assistants: read `AGENTS.md` in the vault root before
> answering from or writing to this vault. It is the operating contract.

**A second brain that grows with every conversation.**

[![License: MIT](https://img.shields.io/badge/License-MIT-blue.svg)](LICENSE)
![Obsidian vault](https://img.shields.io/badge/Obsidian-vault-7C3AED)
![Agents: AGENTS.md](https://img.shields.io/badge/agents-AGENTS.md-black)

**ESPER** stands for **Evidence-Sourced Personal Evolving Repository**: an
Obsidian and plain-Markdown memory template that an AI agent maintains while
you work with it normally. No database, no npm, no indexing service, no
background process.

## Why Esper Brain

- **Memory from normal conversation.** The agent captures durable facts,
  decisions, commitments and corrections without waiting for "remember this".
- **One intake folder.** Drop anything into `00 Inbox/`; the agent files it.
  Manual filing is optional.
- **Evidence over summaries.** Notes are synthesis; originals are preserved
  and consulted for exact amounts, clauses and quotations.
- **Tool-neutral.** The rules live in one `AGENTS.md`. Codex, Claude Code and
  other agents follow the same contract, so you can switch tools without
  migrating memory.
- **Plain files.** Everything is Markdown in folders you own: readable in
  Obsidian, any editor, or Git.
- **Asks only when it matters.** Minor reversible choices stay with the agent;
  deletions, restructuring and external actions require authorization.

## Quick start

> [!IMPORTANT]
> A populated vault is private. Never put personal memory in a public
> repository or a public fork; deleting a file later does not remove it from
> Git history. See [Privacy](#privacy-and-security).

1. **Create your copy.** Click **Use this template** → create a **private**
   repository, or download the archive for a local-only vault (remove `.git`
   if you do not want version control). Record the template commit SHA in
   `template_commit` in `Home.md`, or ask your agent to do it.
2. **Open the folder** as an Obsidian vault and as the workspace of your agent
   (Codex, Claude Code, or another `AGENTS.md`-aware tool), started from the
   vault root.
3. **Start talking**, or drop a file into `00 Inbox/`.

Nothing needs to be installed. There is no onboarding questionnaire: the agent
learns context while doing real work.

Optional: enable the **Daily notes** and **Templates** core plugins in
Obsidian (**Settings → Core plugins**). Their folders are preconfigured.

## How it works

You only put files in the Inbox:

```text
00 Inbox/
  Offer - Client X.pdf
  Signed contract - Client X.pdf
```

If the project is known, the agent keeps the originals with the project and
records the state change, commitments and links on the project card:

```text
01 Projects/
  Client X/
    Client X.md
    Documents/
      Sources/
        Offer.pdf
        Signed contract.pdf
```

If classification is ambiguous, it asks one question and leaves the files in
the Inbox. Reusable material (policies, templates, research) goes to
`03 Resources/`; processed scratch notes and transcripts go to
`04 Archive/Imports/YYYY-MM/` once their knowledge is saved.

Inbox processing runs only while an agent session is active; there is no
watcher. With `inbox_processing: auto` queued material is handled without a
command; with `on_demand` only when you ask.

## Vault structure

```text
.
├── 00 Inbox/          you: the single intake point (+ Inbox.md for quick captures)
├── 01 Projects/       finite efforts, project cards, project documents
├── 02 Areas/          ongoing responsibilities (health, finances, role, home)
├── 03 Resources/      durable knowledge and sources used across projects
├── 04 Archive/        completed projects and processed intake
├── 05 Daily Notes/    dated notes and periodic reviews
├── 06 Meetings/       concise meeting syntheses
├── 07 People/         proportionate context about people
├── 08 Templates/      project, note, meeting and review templates
├── 09 Attachments/    pasted images and embedded media (not an intake queue)
├── .agents/skills/    agent skills (mirrored in .claude/skills/)
├── .claude/           Claude Code settings and skills
├── AGENTS.md          the operating contract for every agent
├── CLAUDE.md          imports AGENTS.md for Claude Code
├── Home.md            entry map
├── Profile.md         your identity, preferences and behavior settings
└── SECURITY.md        privacy and trust boundaries
```

Subfolders are created only when real content needs them. Project documents
can use `Documents/Sources/` (unchanged originals), `Documents/Outputs/`
(deliverables) and `Documents/History/` (superseded material with audit
value). Disposable agent work goes only to the Git-ignored `.tmp/`.

## Agent compatibility

| Tool | How it loads the rules | Notes |
| --- | --- | --- |
| Codex | `AGENTS.md` natively, skills from `.agents/skills/` | `agents/openai.yaml` holds Codex-only skill metadata |
| Claude Code | `CLAUDE.md` → `@AGENTS.md`, skills from `.claude/skills/` | `.claude/settings.json` disables auto memory and asks before risky shell commands |
| Other agents | Any tool that reads `AGENTS.md` | If a host does not auto-load it (mounted folders, remote file tools), the pointer at the top of `README.md`, `Home.md` and `Profile.md` tells the agent to read it first |

The vault is the canonical memory. Host-side memory may hold pointers, never
facts instead of a vault write. Skill files (`SKILL.md` and shared resources)
stay identical in `.agents/skills/` and `.claude/skills/`.

### Hosts that do not load AGENTS.md

Paste this into the host's instructions (project instructions, a global agent
file, or a remote-folder setup):

```text
This folder is an Esper Brain vault: <path to vault>.
Before your first answer from it or write to it, read AGENTS.md,
Profile.md and Home.md in its root, and follow AGENTS.md.
Save durable facts in the vault, not in host-side memory.
```

<details>
<summary>Claude Code settings in detail</summary>

Start Claude Code from the vault root so it loads `.claude/settings.json`,
which:

- sets `autoMemoryEnabled: false`, so the vault stays the only memory store
  (this does not delete earlier auto memory, and a higher-precedence setting
  can override it);
- asks before `rm`, `rmdir`, `git push`, `git reset` and `git clean`.

These prompts add caution; they do not enforce `AGENTS.md`. They do not match
variants such as `/bin/rm` or `git -C . push`, interpreter-run commands, file
edits, moves, sending or connectors, and they are not suppressed by
authorization in `Profile.md` or conversation. An `allow` in
`.claude/settings.local.json` does not override a project `ask`; edit
`.claude/settings.json` in your own copy instead. Checked against the Claude
Code documentation on 2026-10-21.

</details>

## Configuration

All personal settings live in the frontmatter of `Profile.md`; change them by
asking the agent in conversation. The full list of values is in `AGENTS.md`.

| Setting | Values | Default |
| --- | --- | --- |
| `memory_mode` | `proactive` · `explicit` | `proactive` |
| `existing_memory_updates` | `auto` · `ask` · `off` | `auto` |
| `new_project_creation` | `auto` · `ask` · `off` | `ask` |
| `new_note_creation` | `auto` · `ask` · `off` | `auto` |
| `inbox_processing` | `auto` · `on_demand` | `auto` |
| `source_lookup` | `on_demand` · `ask` · `off` | `on_demand` |
| `external_source_retention` | `important_auto` · `ask` · `off` | `important_auto` |
| `technical_activity_reporting` | `quiet` · `verbose` | `quiet` |

`quiet` hides routine notices about files consulted and automatic saves;
`verbose` names them. Neither changes safety: ambiguity, failures, risks and
required confirmations are always reported.

**Software projects.** A project card can point to a repository by a private
`repo` path or a portable `{root, path}` locator resolved through
`repository_roots` in `Profile.md` (empty in the template). Installs, builds,
tests and deployments always need a separate request.

## Migrating an existing vault

Do not overwrite it. Work on a copy, map its folders to this behavior, update
links and verify before replacing the original. A PARA-style structure can
stay; the behavior matters more than identical folder names.

## Updating a vault

Never overwrite vault files wholesale: `AGENTS.md`, skills and templates may
carry deliberate local changes. Ask your agent to:

1. Read `template_commit` from the vault's `Home.md`.
2. If it is empty, compare the vault files with the template's current `main`
   and do not treat differences as errors.
3. Otherwise, compare the template's changes from `template_commit` to the
   current `main` with the vault files.
4. Carry the template changes over while keeping the vault's local changes.
5. Present every conflict that cannot be resolved unambiguously and wait for
   your decision.
6. Write the new commit SHA to `template_commit`.

## Privacy and security

- This repository is the empty public template; your vault is private data.
- Markdown instructions guide agents but are not a sandbox. Any host with
  folder access can read the vault, and cloud models process the text they use.
- Never store passwords, tokens, private keys or recovery codes in the vault.

Read [`SECURITY.md`](SECURITY.md) before connecting a vault to GitHub, a new
model provider, or a cloud-synced folder.

## License

[MIT](LICENSE)
