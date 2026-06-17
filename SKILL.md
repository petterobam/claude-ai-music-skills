---
name: ai-music-skills
description: Complete AI music production workflow for Suno. Use when creating, researching, writing, generating, polishing, mastering, promoting, or releasing AI music albums from one copied skill repository.
argument-hint: [album-name|task]
model: sonnet
effort: medium
prerequisites:
  - album-art-director
  - album-conceptualizer
  - album-dashboard
  - album-ideas
  - clipboard
  - cloud-uploader
  - configure
  - document-hunter
  - explicit-checker
  - genre-creator
  - health-check
  - help
  - import-art
  - import-audio
  - import-track
  - lyric-refiner
  - lyric-reviewer
  - lyric-writer
  - mastering-engineer
  - mix-engineer
  - new-album
  - next-step
  - plagiarism-checker
  - pre-generation-check
  - promo-director
  - promo-reviewer
  - promo-writer
  - promote-idea
  - pronunciation-specialist
  - release-director
  - rename
  - researcher
  - researchers-biographical
  - researchers-financial
  - researchers-gov
  - researchers-historical
  - researchers-journalism
  - researchers-legal
  - researchers-primary-source
  - researchers-security
  - researchers-tech
  - researchers-verifier
  - resume
  - session-start
  - setup
  - sheet-music-publisher
  - suno-engineer
  - test
  - tutorial
  - validate-album
  - verify-sources
  - voice-checker
allowed-tools:
  - Read
  - Bash
  - Glob
  - Grep
  - WebSearch
  - WebFetch
  - bitwize-music-mcp
---

# AI Music Skills

This repository is a single installable Claude skill. Copy the whole repository directory into the Claude skills directory and use this root `SKILL.md` as the entry point.

Use this bundle when the user wants to create, research, write, generate, polish, master, promote, or release AI music with Suno-oriented workflows.

Treat `skills/`, `reference/`, `templates/`, `tools/`, `genres/`, `config/`, and `servers/` as bundled resources that belong to this skill.

---

## Root Path Compatibility

Some bundled modules were originally written for plugin installs and may mention `${CLAUDE_PLUGIN_ROOT}` or `${CLAUDE_PLUGIN_BASE_DIR}`. In this repository-as-skill layout, interpret both as the skill root: the directory containing this root `SKILL.md`.

When a module gives a command with one of those variables, replace it with the absolute path to this copied skill directory before running the command. When a module links to `${CLAUDE_PLUGIN_ROOT}/reference/...`, `${CLAUDE_PLUGIN_ROOT}/templates/...`, `${CLAUDE_PLUGIN_ROOT}/tools/...`, `${CLAUDE_PLUGIN_ROOT}/genres/...`, `${CLAUDE_PLUGIN_ROOT}/config/...`, or `${CLAUDE_PLUGIN_ROOT}/servers/...`, open the matching path inside this same skill directory.

---

## Bundle Loading Protocol

When a task matches a bundled sub-skill:

1. Open that module's `SKILL.md` from `skills/<module>/SKILL.md`.
2. Follow the module instructions exactly.
3. Resolve any files referenced by that module relative to the module directory first.
4. Resolve repository-level references such as `reference/`, `templates/`, `tools/`, `genres/`, `config/`, and `servers/` relative to the directory containing this root `SKILL.md`.
5. Return to this bundle after the module finishes to decide the next phase.

The bundled modules are internal references, not separate top-level skills. Route by opening the relative module files instead of relying on slash commands.

If a bundled module mentions a legacy command like `/bitwize-music:lyric-writer`, translate it to the internal module path `skills/lyric-writer/SKILL.md`. Do the same for any `/bitwize-music:<module>` command that appears in copied templates, references, or module instructions.

---

## Global Rules

- Preserve exact casing and spelling for all user-provided artist names, album names, track titles, lyrics, and labels.
- Read `~/.bitwize-music/config.yaml` fresh before resolving content, audio, document, artist, or override paths.
- Prefer `bitwize-music-mcp` tools for config, albums, tracks, ideas, pending verifications, session state, and cross-scope search when the MCP server is available.
- Fall back to direct files only when MCP is unavailable, raw content is needed, or files must be edited.
- If the user mentions an album name, load `skills/resume/SKILL.md` first.
- If the user wants a new album, load `skills/new-album/SKILL.md` before discussing details.
- If the user wants to promote an idea into an album, load `skills/promote-idea/SKILL.md`.
- Source-based or documentary content must complete research and human source verification before generation.
- After writing or revising lyrics, run the lyric quality flow before generation.
- For mastering, polish with the mix-engineer module first unless the user explicitly skips polish or polished audio already exists.
- Do not skip specialist gates just because the user asks for a later phase.

---

## Main Workflow

### Standard Album

```text
session-start
  -> album-ideas or new-album
  -> album-conceptualizer
  -> lyric-writer
  -> lyric-refiner
  -> pronunciation-specialist
  -> lyric-reviewer
  -> voice-checker
  -> plagiarism-checker
  -> explicit-checker
  -> suno-engineer
  -> pre-generation-check
  -> generate in Suno
  -> import-audio
  -> mix-engineer
  -> mastering-engineer
  -> album-art-director
  -> import-art
  -> promo-director
  -> promo-writer
  -> promo-reviewer
  -> cloud-uploader
  -> release-director
```

### Documentary Album

```text
new-album
  -> album-conceptualizer
  -> researcher
     -> relevant researcher modules
     -> document-hunter when public records are needed
     -> researchers-verifier
  -> verify-sources
  -> writing and production workflow
```

### Regeneration

```text
generated track rejected
  -> log the rejection reason
  -> style issue: suno-engineer
  -> lyric or pronunciation issue: lyric-writer then pronunciation-specialist
  -> Suno interpretation issue: regenerate with the same settings
  -> when accepted, mark the keeper with a check in Generation Log and set status to Final
```

---

## Routing Table

### Session, Setup, and Help

- `session-start` -> [skills/session-start/SKILL.md](skills/session-start/SKILL.md)
- `health-check` -> [skills/health-check/SKILL.md](skills/health-check/SKILL.md)
- `setup` -> [skills/setup/SKILL.md](skills/setup/SKILL.md)
- `configure` -> [skills/configure/SKILL.md](skills/configure/SKILL.md)
- `tutorial` -> [skills/tutorial/SKILL.md](skills/tutorial/SKILL.md)
- `help` -> [skills/help/SKILL.md](skills/help/SKILL.md)
- `test` -> [skills/test/SKILL.md](skills/test/SKILL.md)

### Ideas, Planning, and Navigation

- `album-ideas` -> [skills/album-ideas/SKILL.md](skills/album-ideas/SKILL.md)
- `promote-idea` -> [skills/promote-idea/SKILL.md](skills/promote-idea/SKILL.md)
- `new-album` -> [skills/new-album/SKILL.md](skills/new-album/SKILL.md)
- `album-conceptualizer` -> [skills/album-conceptualizer/SKILL.md](skills/album-conceptualizer/SKILL.md)
- `genre-creator` -> [skills/genre-creator/SKILL.md](skills/genre-creator/SKILL.md)
- `resume` -> [skills/resume/SKILL.md](skills/resume/SKILL.md)
- `next-step` -> [skills/next-step/SKILL.md](skills/next-step/SKILL.md)
- `album-dashboard` -> [skills/album-dashboard/SKILL.md](skills/album-dashboard/SKILL.md)
- `validate-album` -> [skills/validate-album/SKILL.md](skills/validate-album/SKILL.md)
- `rename` -> [skills/rename/SKILL.md](skills/rename/SKILL.md)

### Research and Source Verification

- `researcher` -> [skills/researcher/SKILL.md](skills/researcher/SKILL.md)
- `document-hunter` -> [skills/document-hunter/SKILL.md](skills/document-hunter/SKILL.md)
- `researchers-legal` -> [skills/researchers-legal/SKILL.md](skills/researchers-legal/SKILL.md)
- `researchers-gov` -> [skills/researchers-gov/SKILL.md](skills/researchers-gov/SKILL.md)
- `researchers-tech` -> [skills/researchers-tech/SKILL.md](skills/researchers-tech/SKILL.md)
- `researchers-journalism` -> [skills/researchers-journalism/SKILL.md](skills/researchers-journalism/SKILL.md)
- `researchers-security` -> [skills/researchers-security/SKILL.md](skills/researchers-security/SKILL.md)
- `researchers-financial` -> [skills/researchers-financial/SKILL.md](skills/researchers-financial/SKILL.md)
- `researchers-historical` -> [skills/researchers-historical/SKILL.md](skills/researchers-historical/SKILL.md)
- `researchers-biographical` -> [skills/researchers-biographical/SKILL.md](skills/researchers-biographical/SKILL.md)
- `researchers-primary-source` -> [skills/researchers-primary-source/SKILL.md](skills/researchers-primary-source/SKILL.md)
- `researchers-verifier` -> [skills/researchers-verifier/SKILL.md](skills/researchers-verifier/SKILL.md)
- `verify-sources` -> [skills/verify-sources/SKILL.md](skills/verify-sources/SKILL.md)

### Writing, Suno Prep, and Quality Control

- `lyric-writer` -> [skills/lyric-writer/SKILL.md](skills/lyric-writer/SKILL.md)
- `lyric-refiner` -> [skills/lyric-refiner/SKILL.md](skills/lyric-refiner/SKILL.md)
- `pronunciation-specialist` -> [skills/pronunciation-specialist/SKILL.md](skills/pronunciation-specialist/SKILL.md)
- `lyric-reviewer` -> [skills/lyric-reviewer/SKILL.md](skills/lyric-reviewer/SKILL.md)
- `voice-checker` -> [skills/voice-checker/SKILL.md](skills/voice-checker/SKILL.md)
- `plagiarism-checker` -> [skills/plagiarism-checker/SKILL.md](skills/plagiarism-checker/SKILL.md)
- `explicit-checker` -> [skills/explicit-checker/SKILL.md](skills/explicit-checker/SKILL.md)
- `suno-engineer` -> [skills/suno-engineer/SKILL.md](skills/suno-engineer/SKILL.md)
- `pre-generation-check` -> [skills/pre-generation-check/SKILL.md](skills/pre-generation-check/SKILL.md)
- `clipboard` -> [skills/clipboard/SKILL.md](skills/clipboard/SKILL.md)

### Files, Audio, Artwork, and Sheet Music

- `import-track` -> [skills/import-track/SKILL.md](skills/import-track/SKILL.md)
- `import-audio` -> [skills/import-audio/SKILL.md](skills/import-audio/SKILL.md)
- `import-art` -> [skills/import-art/SKILL.md](skills/import-art/SKILL.md)
- `album-art-director` -> [skills/album-art-director/SKILL.md](skills/album-art-director/SKILL.md)
- `mix-engineer` -> [skills/mix-engineer/SKILL.md](skills/mix-engineer/SKILL.md)
- `mastering-engineer` -> [skills/mastering-engineer/SKILL.md](skills/mastering-engineer/SKILL.md)
- `sheet-music-publisher` -> [skills/sheet-music-publisher/SKILL.md](skills/sheet-music-publisher/SKILL.md)

### Promotion, Cloud, and Release

- `promo-director` -> [skills/promo-director/SKILL.md](skills/promo-director/SKILL.md)
- `promo-writer` -> [skills/promo-writer/SKILL.md](skills/promo-writer/SKILL.md)
- `promo-reviewer` -> [skills/promo-reviewer/SKILL.md](skills/promo-reviewer/SKILL.md)
- `cloud-uploader` -> [skills/cloud-uploader/SKILL.md](skills/cloud-uploader/SKILL.md)
- `release-director` -> [skills/release-director/SKILL.md](skills/release-director/SKILL.md)

---

## Output Contract

When coordinating the bundle, always include:

1. The inferred phase.
2. The sub-skill module being loaded or recommended.
3. Any blocking gate, especially setup, config, unverified sources, unresolved pronunciation, failed QC, missing audio, missing artwork, or release readiness gaps.
4. The next concrete action.

Keep responses focused on moving the album forward.
