# Integration Guide
How to inject the optimized prompt into various LLMs and AI editors.

---

## LLMs

### Claude (Anthropic)

**Web (claude.ai):**
1. Go to claude.ai → Settings → Projects
2. Create/select project → "Project Instructions"
3. Paste the prompt

**Claude Code (CLI):**
1. Create `CLAUDE.md` in project root
2. Paste prompt content
3. Auto-loaded as context

**Direct:**
- Paste prompt as first message in a new chat

---

### ChatGPT / GPT-4

**Custom GPTs:**
1. chat.openai.com → Explore GPTs → Create
2. Configure tab → "Instructions" field
3. Paste the prompt

**Temporary:**
- Paste prompt as first message, follow with task

> No native dotfile support — web only.

---

### GitHub Copilot (VS Code)

1. VS Code → Settings → search `copilot.instructions`
2. Or create `.github/copilot-instructions.md` in repo root
3. Paste prompt content

---

### Codex Editor (GitHub)

GitHub's agentic coding editor — separate from Copilot.

1. Create `codex.md` in project root
2. Paste prompt content
3. Auto-loaded as system context

> Distinct from `.github/copilot-instructions.md`.

---

### Gemini (Google)

**Gems:**
1. gemini.google.com → Gem Manager → New Gem
2. "Instructions" field → paste prompt

> No native dotfile support — web only.

---

### Deepseek / Qwen / GLM / Kimi

- **Web:** Paste prompt as first message
- **API:** Pass prompt in `system` role / field

> No native dotfile support for any of these.

---

## AI Editors

### Cursor

1. Settings (⌘/Ctrl+,) → General → "Rules for AI"
2. Or create `.cursorrules` in project root
3. Paste prompt content

---

### Windsurf

1. Settings → Cascade → "System Prompt" or "Memory"
2. Or create `.windsurf/rules.md` in project root
3. Paste prompt content

---

### Opencode

1. Settings → AI Configuration → System Instructions
2. Paste prompt → Save

---

### Antigravity

1. Project settings → AI Rules
2. Or create `.antigravity/rules` in project root
3. Paste prompt content

---

## Dotfile Reference

| Tool | File | Location |
|------|------|----------|
| Claude Code | `CLAUDE.md` | Project root |
| Cursor | `.cursorrules` | Project root |
| Windsurf | `.windsurf/rules.md` | Project root |
| Codex Editor | `codex.md` | Project root |
| GitHub Copilot | `.github/copilot-instructions.md` | `.github/` folder |
| Antigravity | `.antigravity/rules` | Project root |

**Web-only (no dotfile support):** ChatGPT, Gemini, Deepseek, Qwen, GLM, Kimi

---

## Quick Reference

| Platform | Injection Method | File |
|----------|-----------------|------|
| Claude | Project Instructions / CLAUDE.md | Web UI / project root |
| ChatGPT | Custom GPT Instructions | Web UI |
| GitHub Copilot | VS Code settings | `.github/copilot-instructions.md` |
| Codex Editor | Auto-load | `codex.md` |
| Gemini | Gems | Web UI |
| Deepseek / Qwen / GLM / Kimi | System message | Web UI / API |
| Cursor | Rules for AI | `.cursorrules` |
| Windsurf | System Prompt | `.windsurf/rules.md` |
| Opencode | System Instructions | Settings |
| Antigravity | AI Rules | `.antigravity/rules` |

---

## Tips

- **Dotfiles take priority** over manual paste — use them for persistent projects
- **Priority order:** editor-native rules > project dotfile > global settings
- **Verify injection:** ask "What rules are you following?" after setup