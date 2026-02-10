# claude-soul

English | [中文](README_CN.md)

Give your Claude Code a persistent soul and evolving memory.

Two files. No framework. No dependencies. Clone → restart → it just works.

## What is this?

Claude Code resets every session. It doesn't remember your preferences, your working style, or the lessons learned from your last collaboration.

**claude-soul** fixes this with two Markdown files:

| File | Role |
|------|------|
| `CLAUDE.md` | **Soul** — personality, principles, work practices, boundaries. Defines *who* your AI collaborator is. |
| `COGNITION.md` | **Cognition** — behavioral portrait of *you*. Built through observation over time. Dual-purpose: helps Claude calibrate, and gives you a mirror to see your own patterns. |

The soul provides a strong default from day one. The cognition starts nearly empty and fills in as Claude observes your patterns — how you make decisions, what excites you, what you skip over, when you want control. It also serves as a self-reflection tool: reading your own cognition file can reveal habits and blind spots you weren't aware of.

## Quick Start

> **Already have a `~/.claude/CLAUDE.md`?** Back it up before installing:
> ```bash
> cp ~/.claude/CLAUDE.md ~/.claude/CLAUDE.md.bak
> ```
> Claude will detect the `.bak` file during onboarding and ask if you want to migrate useful content from it.

### Option A: Tell Claude to set it up

Open Claude Code and send:

```
Clone https://github.com/MidnightV1/claude-soul into ~/.claude/ and remind me to restart the session.
```

### Option B: Manual install

```bash
# Back up existing CLAUDE.md if you have one
[ -f ~/.claude/CLAUDE.md ] && cp ~/.claude/CLAUDE.md ~/.claude/CLAUDE.md.bak

# Clone soul files
cd ~/.claude \
  && git init \
  && git remote add origin https://github.com/MidnightV1/claude-soul.git \
  && git fetch origin \
  && git checkout origin/main -- CLAUDE.md COGNITION.md .gitignore
```

Then **restart your Claude Code session**. Claude will read the soul file and start the onboarding conversation.

## How it works

### First session

Claude reads `CLAUDE.md`, notices the "What I Don't Know Yet" section, and naturally asks a few key questions — your name, language, communication style, autonomy preference. Based on your answers, it personalizes the soul file. No questionnaire, no ceremony.

### Every session after

Claude loads both files on startup. The soul guides behavior. The cognition file provides context about you. Together they eliminate the cold-start problem.

### Continuous evolution

A meta-rule in the soul file instructs Claude to reflect after each task milestone:

- Effective patterns → update soul or cognition
- Replace, don't append → files stay lean
- Sync to git (optional) → your soul is version-controlled

## Cloud sync (optional)

If you want your soul and cognition backed up and portable across machines:

1. Create a GitHub repo (private recommended — see note below)
2. During onboarding, tell Claude you want git sync enabled
3. Claude will set up the remote and push after each update

The `.gitignore` is pre-configured to only track `CLAUDE.md`, `COGNITION.md`, `README.md`, and `.gitignore`. Everything else in `~/.claude/` (credentials, cache, telemetry) is excluded.

> **Privacy note:** `COGNITION.md` accumulates a behavioral profile of you — decision patterns, emotional signals, delegation habits. If your repo is public, this data is visible to anyone. Use a private repo if this concerns you. GitHub Free accounts include unlimited private repos.

## File structure

```
~/.claude/
├── .gitignore       ← whitelist-based, only tracks soul files
├── CLAUDE.md        ← soul (personality + work practices + onboarding logic)
├── COGNITION.md     ← cognition (behavioral model of you, evolves over time)
└── ...              ← other Claude Code files (ignored by git)
```

## Design philosophy

- **Two files, not six.** Minimal surface area, maximum impact.
- **Convention over configuration.** Claude Code already reads `~/.claude/CLAUDE.md`. We just put the right content there.
- **Observe, don't interrogate.** Most of the cognition file is filled through silent observation, not questionnaires.
- **Replace, don't append.** Files are kept lean through overwrite, not accumulation.
- **Works on day one, gets better over time.** The soul ships with universal engineering defaults. Personalization is additive.

## Related projects

The pattern of accumulating user cognition through conversation was first practiced in [sovi-demo](https://github.com/MidnightV1/sovi-demo), where system prompts silently build user profiles through observation rather than explicit collection. claude-soul extracts this pattern from a specific application into a general-purpose, portable AI collaboration infrastructure.

[OpenClaw](https://github.com/nicekid1/OpenClaw) explores a similar direction — giving AI persistent identity through file systems. Different paths, same destination.

## License

MIT
