---
name: review-esper-brain
description: "Read-only health review of an Esper Brain Obsidian vault: memory consistency, Inbox queue, skill mirrors, template drift and file hygiene. Use only when the user asks to review or check the vault."
---

# Review Esper Brain

Read root `AGENTS.md`, `Profile.md`, and `Home.md`. This skill is read-only:
it reports in the conversation and writes no file. Root instructions and active
Profile controls remain authoritative.

During the review, only report the Inbox queue; never process it, even with
`inbox_processing: auto`. This does not change the Profile setting.

Run the checks in this order:

1. Memory consistency. For each project card in `01 Projects/`, check that its
   `status` matches the section where `01 Projects/Projects.md` lists it, that
   the card does not describe contradictory states, and that a card with
   `status: active` has a non-empty "Next action" section.
2. Inbox. List every file in `00 Inbox/` other than `Inbox.md`, and every item
   under "Open" in `00 Inbox/Inbox.md`, with its date and the reason it is
   waiting.
3. Skills. Every skill exists in both `.agents/skills/` and `.claude/skills/`,
   and their shared files are identical. Agent-specific metadata such as
   `agents/openai.yaml` is expected in one copy only.
4. Template drift. For `AGENTS.md`, `CLAUDE.md`, `SECURITY.md`, skills, and
   `08 Templates/`, report two separate results:
   - local changes: the vault files compared with the template at
     `template_commit` from `Home.md`;
   - pending template updates: the template's changes from `template_commit`
     to its current `main`.
   When `template_commit` is empty, report one result: the vault files compared
   with the template's current `main`. Do not treat differences as errors and
   do not update any file.
5. File hygiene. Report the total size of `.tmp/`, the number of its entries
   older than 30 days, and root entries outside the vault structure. Standard
   root entries are not findings: the folders listed in `AGENTS.md`, the
   template files (`AGENTS.md`, `CLAUDE.md`, `Home.md`, `Profile.md`,
   `README.md`, `SECURITY.md`, `LICENSE`, `.gitignore`, `.gitattributes`),
   configuration folders (`.agents/`, `.claude/`, `.obsidian/`, `.github/`),
   version control (`.git/`), `.tmp/`, `.trash/`, and operating-system files
   such as `.DS_Store`. Report every other root entry, especially folders with
   content or tool output.

If a file or the template cannot be read, report it and continue. Group the
report by check, put problems before passing checks, and propose fixes without
applying them. Fixes follow the existing Profile controls; deletion and moves
require separate authorization.
