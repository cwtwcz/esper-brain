# Esper Brain

> **A second brain memory system that grows with every conversation.**

**ESPER** stands for **Evidence-Sourced Personal Evolving Repository**.

A small, effective Obsidian and Markdown memory template built around natural
conversation. No database, npm, indexing service, or background process.

## Privacy first

This repository contains only the empty public template. A personal vault will
contain private memory and should stay local or in a repository whose visibility
and collaborators you have deliberately chosen.

- On GitHub, use **Use this template**, create a **private** repository, and
  verify its visibility before adding personal information.
- For a local-only vault, download the template as an archive and keep it
  outside Git, or remove its Git metadata before use.
- Do not create a public fork for personal memory. Deleting a committed secret
  or note later does not remove it from Git history.

## Start in three steps

1. Create a private repository from the template, or download a local copy.
2. Open the repository root as an Obsidian vault and as a Codex or Claude Code
   workspace.
3. Start talking normally, or place a file in `00 Inbox/`.

Nothing needs to be installed. The assistant learns useful context while doing
real work instead of forcing an onboarding questionnaire or filing ritual.

Optional Obsidian shortcuts: enable the **Daily notes** and **Templates** core
plugins under **Settings → Core plugins**. Their folders are already configured;
Esper Brain works without them.

## The only folder you need to manage

Put every unprocessed note, transcript, screenshot, PDF, or document in
`00 Inbox/`. You may browse and edit the entire vault, but manual filing is
optional. The agent and Obsidian handle the rest:

- `00 Inbox/` — **user:** the single intake point. `Inbox.md` also holds short
  conversation captures and unresolved items.
- `01 Projects/` — **agent:** finite efforts, project cards, and documents that
  belong to one project.
- `02 Areas/` — **agent:** ongoing responsibilities such as health, finances,
  family, a professional role, or maintaining a home.
- `03 Resources/` — **agent:** durable knowledge and authoritative sources used
  across multiple projects.
- `04 Archive/` — **agent:** completed projects, inactive material, and
  processed intake retained for provenance.
- `05 Daily Notes/` — **Obsidian or agent:** dated notes and periodic reviews.
- `06 Meetings/` — **agent:** concise meeting syntheses; original transcripts
  normally go to Archive.
- `07 People/` — **agent:** useful, proportionate context about people.
- `08 Templates/` — **system:** reusable project, note, meeting, and review
  shapes.
- `09 Attachments/` — **Obsidian:** pasted images and embedded media. It is not
  an intake queue or document library.

Top-level folders are pre-created. Subfolders are created only when real content
needs them.

Disposable agent work belongs only in the hidden root `.tmp/`, which may be
cleared at any time and is ignored by Git. Durable project material uses an
optional functional structure under `Documents/`: unchanged originals in
`Sources/`, created deliverables in `Outputs/`, and superseded material in
`History/` only when it still has audit or decision value.

## Example: an offer and a signed contract

The user only does this:

```text
00 Inbox/
  Offer - Client X.pdf
  Signed contract - Client X.pdf
```

If the project is known, the agent preserves the originals next to the project:

```text
01 Projects/
  Client X/
    Client X.md
    Documents/
      Sources/
        Offer.pdf
        Signed contract.pdf
```

The project card receives the durable state change, important commitments, and
links to the exact source files. If the project is unknown or classification is
ambiguous, the agent asks one question and leaves the files in Inbox.

A company-wide policy, reusable contract template, or research source belongs
in `03 Resources/`, not inside one project. A processed scratch note,
transcript, or screenshot normally goes to `04 Archive/Imports/YYYY-MM/` after
its useful knowledge has been saved.

## Natural memory

The agent does not wait for “remember this”. Before finishing a substantive
conversation, it captures clear durable identity, relationship, project,
decision, commitment, preference, and correction deltas.

- Existing memory receives small, unambiguous updates automatically.
- A clearly useful non-project note may be created automatically. A new project
  card still requires consent by default.
- Named people, companies, products, and projects are resolved through Profile,
  maps, and linked canonical notes before generic context is used.
- Casual chat, unsupported inference, secrets, and full transcripts are not
  stored as memory.
- Canonical notes emphasize current useful state. Superseded research is kept
  only when it explains a decision, commitment, audit trail, or recurring
  pattern.
- The assistant answers the topic first and follows the configured technical
  activity reporting mode.

There is no hidden watcher. `inbox_processing: auto` handles queued material
without a special command while Codex or Claude Code is active;
`inbox_processing: on_demand` does not inspect the queue until requested.

## Profile controls

`Profile.md` contains safe defaults and is the only place that should hold
personal behavior settings or machine-local repository roots. The supported
policy values are documented in `AGENTS.md`; change them naturally in
conversation rather than learning commands. In particular:

- most action controls use `auto`, `ask`, or `off`;
- `inbox_processing: auto | on_demand` controls whether Inbox processing starts
  during an active session or only after an explicit request;
- `memory_mode: proactive | explicit` controls whether ordinary conversation
  may produce durable memory.

## Technical activity reporting

`Profile.md` contains the `technical_activity_reporting` switch:

- `quiet` (default) hides routine notices about files consulted, automatic
  unambiguous saves, and the absence of changes.
- `verbose` shows the exact memory and source files consulted and changed, and
  says when nothing was changed.

This setting changes narration, not safety or consent. The assistant still asks
when a write is ambiguous or requires approval, reports failures and risks, and
provides source citations when they support the answer. An explicit request for
an activity report overrides the setting for that response.

## Originals preserve precision

Markdown notes are synthesis, not a replacement for evidence. For an exact
clause, amount, requirement, version, or quotation, the agent returns to the
original local file or an authorized connected document. It uses an appropriate
PDF, document, spreadsheet, or image skill and reports the best available page,
section, cell, timestamp, or OCR limitation.

## Software projects

A project card may contain a direct private `repo` path or a portable
`{root, path}` locator. Portable roots resolve through the private
`repository_roots` mapping in `Profile.md`; the public template leaves this map
empty. Source-level verification starts with repository `AGENTS.md` or
`CLAUDE.md`, the relevant manifest, root README, directly relevant docs,
read-only Git state, and only then targeted code. Installs, builds, tests, and
deployments require a separate request.

## Existing vaults

Do not overwrite an existing vault. Work on a copy, preserve its content, map
its folders to this behavior, update links, and verify before replacing the
original. A familiar PARA-style structure may remain; the behavior matters more
than identical folder names.

## Security boundary

Markdown instructions guide behavior but are not a sandbox. A host with folder
access can technically read its contents, and a cloud model may process text
used for an answer. Do not store passwords, tokens, private keys, or recovery
codes in the vault. See `SECURITY.md` before connecting a vault to GitHub or a
new model provider.

## License

MIT. See `LICENSE`.
