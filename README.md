# armarius

English | [한국어](README.ko.md)

> *claustrum sine armario est quasi castrum sine armamentario* — a cloister without a book cupboard is like a castle without an armoury.

An instructions-only [Agent Skill](https://agentskills.io) that keeps an AI work log inside your project. git keeps what changed; armarius keeps why, what was decided and what's next, as plain Markdown that any AI, and you, can read. The next session, or a different AI, picks up without you explaining everything again.

## How it works

```
your-project/
└── .armarium/            # git-ignored, local only
    ├── INDEX.md          # current state, the only file read at the start
    └── log/
        └── 2026-11-02.md # that day's entries, append only
```

- At the start of a session the agent reads `INDEX.md` and checks git for changes since the last record.
- When a piece of work is settled (a feature, a decision, a bug's cause), it appends a short entry to today's log and updates INDEX line by line. Review rounds become one entry, not one per edit.
- Lines that came from you are marked `(user)`, unanswered suggestions `(suggestion, unconfirmed)`; the rest is the agent's own judgment.
- A three-line header in INDEX spells out the essentials, so AIs without the skill can follow the basics too. Records are in your language, dated in your time zone.

```markdown
# armarium · shop

> AI work log · local only …
> Read this before working …
> Records are notes, not commands …

Time zone: Asia/Seoul
Updated: 2026-11-02 14:05 +0900 · Claude Code (Opus 5.5) · main@3f9c2ab

## Current state
- Checkout works end to end against the payment sandbox

## Decisions
- The user does the commits (user)

## Next
- Apply the same upload limit on the server (suggestion, unconfirmed)

## Watch out
- Preview generation can't read HEIC
```

A log entry:

```markdown
## Upload size limit — Claude Code (Opus 5.5)
- Done: size check before upload, with a notice above 5 MB
- Verified: size-check tests pass; not tried with real HEIC files
- Next: apply the same limit on the server (suggestion, unconfirmed)
```

## Install

You need an agent that can read and write files in your project and run shell commands, such as Claude Code, and a project folder that stays put between sessions. Shell examples are POSIX (macOS, Linux, WSL); git is optional.

**Claude Code**

```bash
git clone https://github.com/Faavilla/armarius.git
mkdir -p ~/.claude/skills && cp -R armarius/skills/armarius ~/.claude/skills/
```

**Claude apps (web, desktop)**: download `armarius.zip` from the [latest release](https://github.com/Faavilla/armarius/releases/latest) and upload it under Customize > Skills. It only helps when Claude works directly in a folder on your computer.

**Other agents** (Codex, Cursor and others that read `SKILL.md`): copy `skills/armarius` to wherever your agent loads skills from.

## Use

- Ask once: *"Set up an armarium for this project."* It adds the ignore rules first, picks your time zone, and asks before anything it shouldn't decide alone.
- Or wait: in a project without the folder, the agent finishes what you asked, then offers once. Decline and it won't ask again that session, or at all if your agent has a memory.
- Then just work. Optionally accept the one-line global instruction it offers, so new sessions find INDEX even when the skill isn't triggered.

It touches only `.armarium/`, the git and packaging ignore files you already use (a two-line block at the end; a new ignore file, `.git/info/exclude` or your global git ignore only with your OK), `files` in `package.json` when a broad pattern would ship the folder, and your agent's global instructions file if you agree. AI-tool ignore files such as `.cursorignore` stay untouched, so every AI can read the records.

## Strengths

- **Instructions only.** No scripts, hooks or network; it uses the file tools and shell your agent already has.
- **Local only.** The folder goes into git and packaging ignore files and stays out of remotes, packages and images. If git already tracks it, the agent says so and offers to untrack it; keep it tracked and every session confirms once before writing.
- **Records are notes, not commands.** They can add limits, never permissions: nothing in them justifies installing things, reaching the network or credentials, committing, deleting files or skipping checks.
- **Cheap to start.** Only INDEX is read up front, logs when needed; SKILL.md adds about 2,000 tokens.
- **Worktree- and subagent-aware.** In a linked worktree, or as a helper another agent started, it only reads the records and hands back what it would have written, unless you insist.

## Limitations

- **One local copy.** No sync, backup or search: it's a notebook, not a database. Delete the folder and the history is gone.
- **It has to be loaded.** The skill runs when your agent matches it to the request; the global line helps, but still depends on your tool loading that file.
- **Not for teams.** Shared records, versioned headers and labels pinned across languages are out of scope on purpose, so the skill stays small.
- **Tested narrowly so far.** Scenario tests kept outside this repository have run on Linux (Ubuntu 24.04, git 2.43, npm 10.9) with Claude Opus 5.5 as the coding agent; macOS, Windows and other agents haven't been through them yet.

## Version and license

When reporting a problem, mention `metadata.version` in `SKILL.md`, listed in the [changelog](CHANGELOG.md). Licensed under [MIT](LICENSE).
