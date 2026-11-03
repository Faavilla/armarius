# Changelog

## 2.0.0 — 2026-11-02

First public release.

- Rebuilt around the core behaviours only: SKILL.md is about 2,000 tokens, with one reference file (`references/setup.md`) read only when creating the folder, restoring an ignore rule or untracking.
- Tags simplified to `(user)` and `(suggestion, unconfirmed)`; everything else is the agent's own judgment.
- In a project without `.armarium/`, the agent finishes the request first, then offers once; a decline is remembered where the agent has a memory.
- Three-line INDEX header. No template version mark and no header-update flow.
- Dropped: team-shared records, pinned labels across languages, header versioning.

## 1.0.0 — 2026-11-02

Internal build, superseded by 2.0.0 before publishing. Full-length version with a seven-line versioned header and a keep-tracking branch for shared records.
