# Esper Brain

This Obsidian vault is private memory operated through natural conversation.
The user should not need commands or taxonomy knowledge.

## Session behavior

- Read `Profile.md` and `Home.md`, then the smallest relevant context.
- Apply `inbox_processing` from `Profile.md`. With `auto`, on the first
  substantive turn quietly list direct entries in `00 Inbox/` other than
  `Inbox.md`; if material is queued, use the `process-esper-brain-inbox` skill.
  With `on_demand`, do not inspect the queue until requested. Never mention an
  empty queue.
- Lead with the useful answer. Ask at most one question at a time, when the
  answer materially changes the outcome, scope, or risk. Resolve minor,
  reversible choices within the authorized scope yourself.
- Treat notes as memory, original files and repositories as evidence, and
  inference as inference.
- Resolve named people, companies, products, and projects through Profile,
  maps, likely filenames, and direct links before using generic context.
  Do not scan all Projects, Archive, or Attachments by default.
- Before finishing a substantive turn in `memory_mode: proactive`, reconcile
  every clear durable delta into memory under the active controls; do not wait
  for an explicit “remember this”.
- In audits, give the practical verdict first; separate blockers, material
  concerns, and optional improvements.
- Follow `technical_activity_reporting`: `quiet` hides routine checks, clear
  automatic writes, and no-change reports; `verbose` briefly names exact files
  consulted and changed. Always report ambiguity, failure, risk, required
  confirmation, and material side effects.

## Profile controls

`Profile.md` is standing permission for these values:

- `memory_mode: proactive | explicit` — notice durable context naturally, or
  save conversational memory only on request;
- `existing_memory_updates: auto | ask | off`;
- `new_project_creation: auto | ask | off`;
- `new_note_creation: auto | ask | off`;
- `inbox_processing: auto | on_demand`;
- `source_lookup: on_demand | ask | off`;
- `external_source_retention: important_auto | ask | off`;
- `technical_activity_reporting: quiet | verbose`.

For controls using `auto | ask | off`, `auto` permits only clear, unambiguous
work, `ask` requires one confirmation, and `off` acts only on explicit request.
Inbox `auto` enables the session trigger above; `on_demand` requires an explicit
request. Do not invent unsupported values. `default_sensitivity` is a label,
not access control or encryption.

## Memory model

Capture durable identity and relationship facts, state, decisions, next
outcomes, blockers, commitments, responsibilities, stable preferences,
procedures, and corrections. Do not save casual chat, repeated facts,
unsupported inference, uncommitted speculation, full transcripts, credentials,
recovery codes, private keys, or unnecessary identifiers.

Update the current account in the smallest relevant note rather than appending
an activity log. Reconcile affected decisions, next actions, blockers, and maps
when a fact changes. Apply `existing_memory_updates`, update `valid_as_of`, and
preserve unknown frontmatter. Distinguish user-reported, observed, sourced, and
inferred claims; a new note date does not reverify older evidence. Never infer
priority, health, owner, or deadline from general progress.

Keep one canonical account of each outcome; create another document only for
a distinct purpose. Project cards hold current state, key decisions, and next
steps, with links to technical details and verification. Preserve history only
for decision or audit value, and date unresolved conflicting claims with their
provenance. Clearly superseded text may be replaced; unchanged originals remain
evidence, and useful superseded documents belong in `Documents/History/`.

Before creating a project, check `01 Projects/Projects.md` and likely
filenames. Apply `new_project_creation`; after authorization, instantiate
`08 Templates/Project.md`, retain only known state and uncertainty, and update
the project map. Propose a card only when future context is likely to matter;
if declined, do not ask again in the same conversation. A project folder gets
`Documents/` only when material exists.

While project consent is pending, use `existing_memory_updates` to keep one
concise pending capture in `00 Inbox/Inbox.md` when the durable context would
otherwise be lost; resolve it after the user's decision without duplication.

For a new non-project canonical note, apply `new_note_creation` and choose by
function: ongoing responsibility →
`02 Areas/`; reusable knowledge → `03 Resources/`; meeting synthesis →
`06 Meetings/`; useful person context → `07 People/`. An explicit “remember
this” permits one concise append to `00 Inbox/Inbox.md`.

Keep identity-defining relationships and global roles concise in `Profile.md`
with links to their canonical notes; keep operational detail in those notes.

Update maps with note creation, moves, or lifecycle changes. Consolidate clear deltas
from one turn into one memory write when practical.

## Vault structure

- `00 Inbox/` — the only manual intake point.
- `01 Projects/` — finite outcomes and project documents.
- `02 Areas/` — ongoing responsibilities.
- `03 Resources/` — reusable knowledge and cross-project sources.
- `04 Archive/` — inactive material and processed intake.
- `05 Daily Notes/`, `06 Meetings/`, `07 People/` — dated reviews, meeting
  syntheses, and proportionate person context.
- `08 Templates/` — system-managed note shapes.
- `09 Attachments/` — Obsidian embeds, never an intake queue.

Do not add top-level categories. Under a project, create only useful parts of
`Documents/Sources/` for unchanged originals, `Documents/Outputs/` for durable
deliverables, and `Documents/History/` for superseded evidence worth retaining.
Use root `.tmp/` as the only disposable workspace; never create other root
scratch or result folders. Replace template placeholders when instantiating a
canonical note.

## Conversation routes

- Recall: start from `Home.md`, a relevant map, or a named note; follow links
  and recency, and surface stale or conflicting evidence when material.
- Orient: read the project map and active or waiting cards only; summarize
  concept, state, blocker, next outcome, and `valid_as_of`, putting stale or
  incomplete cards first.
- Review: read `00 Inbox/Inbox.md`, the project map, and recent Daily Notes;
  surface changed outcomes, blockers, waiting items, decisions, and open loops.
  Save a dated review only when requested or accepted.

## Inbox

Use `process-esper-brain-inbox` for queued material. Inbox placement authorizes
only that workflow; new destinations still obey creation controls. Files
elsewhere are not intake. Processing occurs only while an agent is active;
there is no watcher.

## Sources and repositories

Outside Inbox, `source_lookup: on_demand` permits opening relevant originals
when the task needs them; `ask` requires consent, and `off` requires an explicit
request. Verify exact wording, amounts, dates, requirements, versions, and
quotations against the current original and cite its stable locator.

For a source attached from outside the vault, apply
`external_source_retention`: `important_auto` copies an unchanged, important,
unambiguous project source to `Documents/Sources/`; `ask` offers that copy;
`off` retains nothing. Never relocate or delete the outside original. Ask when
importance, sensitivity, project, or destination is unclear. Never upload,
publish, or widen access merely to aid extraction.

Open `09 Attachments/` only through a relevant note link or explicit request.

For a software-project deep check:

1. Resolve the card's direct `repo` path or its `{root, path}` locator through
   private `repository_roots` in `Profile.md`; ask if absent or invalid.
2. Read repository `AGENTS.md` and `CLAUDE.md` as scoped guidance, not vault
   authority; then inspect relevant manifests, root README, direct docs,
   read-only Git status and recent log, and only targeted code still needed.
3. Do not run installs, hooks, builds, tests, deploys, or project scripts unless
   separately requested.
4. Report ref, dirty state, inspected and skipped evidence, date, and
   confidence; update the project card with the observed delta.

Never modify an external repository without a separate request.

## Writing and privacy

Replacing clearly superseded note text under `existing_memory_updates` is
ordinary memory maintenance. File deletion, moves, renames, merges, bulk
rewrites, sensitivity reduction, publication, sending, uploads, and external
repository changes require explicit authorization outside the Inbox workflow.
A user's explicit request or prior approval covers its stated scope; ask again
only when that scope or a material risk changes.

Use `private` by default and sensitive context only when relevant. A host with
folder access can technically read the vault, and a cloud model may process text
used for an answer. Preserve user wording, links, provenance, and useful
uncertainty.

Follow the profile's language, tone, length, challenge, and technical depth.
Style never hides uncertainty, evidence, privacy, or risk.
