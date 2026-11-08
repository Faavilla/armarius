# Changelog

## 2.1.0 — 2026-11-08

- Subagents and linked worktrees now skip the other start-up checks and the setup offer; they don't write to `.armarium/` unless you insist, and hand back a draft entry with the date and branch. Worktrees of a bare repository no longer count as linked.
- Before any `git clean`, the agent previews it with `-n` and stops if it lists anything in the folder, since `-x` or `-X` with a path can delete it even without `-d`. The INDEX header says this too, and tells subagents and other worktrees not to write.
- The untracking warning now covers how old commits can overwrite or delete the local records or put them back under git, and how to look at old commits safely.
- A misspelled time zone name no longer goes unnoticed, trimming INDEX never drops anything recorded nowhere else, and a new `.npmignore` no longer leaves out the build output the package needs.
- Smaller changes: a user decision the code contradicts stays in INDEX while the agent asks; the ignore block isn't added twice; setup always offers the global line, which now says where a linked worktree's records are.
- Existing INDEX files and accepted global lines keep their wording; only new ones get the updated text.

## 2.0.0 — 2026-11-03

First public release of armarius, an instructions-only Agent Skill that keeps an AI work log in your project's git-ignored `.armarium/` folder.

- Reads `INDEX.md` at the start of a session, appends dated log entries, and updates INDEX as work is settled.
- Local only: the folder goes into git and packaging ignore files. Records are notes, never permissions.
- In a project without the folder, it finishes your request first, then offers once.

## 1.0.0 — 2026-11-02

Internal build, superseded by 2.0.0 before publishing. Full-length version with a seven-line versioned header and team-shared records.
