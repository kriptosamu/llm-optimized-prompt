# Integration Guide
How to inject the optimized prompt into various LLMs and AI editors.

> **Last verified:** May 2025. Tool integrations evolve rapidly — verify against official docs if in doubt.

---

## LLMs

### Claude (Anthropic)

**Web (claude.ai):**
1. Go to claude.ai → Settings → Projects
2. Create/select project → "Project Instructions"
3. Paste the prompt

**Direct:**
- Paste prompt as first message in a new chat

---

### ChatGPT / GPT-4

**Custom GPTs:**
1. chatgpt.com → Explore GPTs → Create
2. Configure tab → "Instructions" field
3. Paste the prompt

**Temporary:**
- Paste prompt as first message, follow with task

> No native dotfile support — web only.

---

### Gemini (Google)

**Gems:**
1. gemini.google.com → Gem Manager → New Gem
2. "Instructions" field → paste prompt

**Google AI Studio:**
- System Instructions field → paste prompt

> No native dotfile support — web and API only.

---

### Deepseek / Qwen / GLM / Kimi

- **Web:** Paste prompt as first message
- **API:** Pass prompt in `system` role / field

> No native dotfile support for any of these.

---

## AI Editors & CLI Agents

### Claude Code (CLI)

Anthropic's agentic CLI coding tool.

1. Create `CLAUDE.md` in project root
2. Paste prompt content
3. Auto-loaded as context

> Also supports `AGENTS.md` (cross-tool convention).

---

### Cursor

1. Settings (Ctrl+,) → General → "Rules for AI"
2. Or create `.cursor/rules/*.mdc` files in project root (recommended)
3. Paste prompt content

> **Legacy:** `.cursorrules` at project root still works but is deprecated. Migrate to `.cursor/rules/` for scoped, modular rules with YAML frontmatter.

---

### Windsurf

1. Settings → Cascade → Customizations → Rules
2. Or create files in `.windsurf/rules/` directory in project root
3. Paste prompt content

> **Legacy:** `.windsurfrules` at project root is supported but `.windsurf/rules/*.md` is recommended for modularity.

---

### Codex CLI (OpenAI)

OpenAI's open-source terminal-based AI coding agent.

1. Create `AGENTS.md` in project root
2. Paste prompt content
3. Auto-loaded as system context

> `AGENTS.md` is the cross-tool standard — also supported by Gemini CLI and Claude Code.

---

### GitHub Copilot (VS Code)

1. VS Code → Settings → search `copilot.instructions`
2. Or create `.github/copilot-instructions.md` in repo root
3. Paste prompt content

---

### Opencode

1. Settings → AI Configuration → System Instructions
2. Paste prompt → Save

> No documented dotfile support as of last verification.

---

### Antigravity (Google)

1. Project settings → AI Rules
2. Or use Gemini-compatible conventions (`GEMINI.md` / `AGENTS.md` in project root)
3. Paste prompt content

> Dotfile conventions may vary — verify against current documentation.

---

## Dotfile Reference

| Tool | File | Location | Status |
|------|------|----------|--------|
| Claude Code | `CLAUDE.md` | Project root | ✅ Current |
| Codex CLI | `AGENTS.md` | Project root | ✅ Current |
| Cursor | `.cursor/rules/*.mdc` | Project root | ✅ Current |
| Cursor (legacy) | `.cursorrules` | Project root | ⚠️ Deprecated |
| Windsurf | `.windsurf/rules/*.md` | `.windsurf/rules/` | ✅ Current |
| Windsurf (legacy) | `.windsurfrules` | Project root | ⚠️ Legacy |
| GitHub Copilot | `.github/copilot-instructions.md` | `.github/` folder | ✅ Current |
| Cross-tool | `AGENTS.md` | Project root | ✅ Codex, Gemini CLI, Claude Code |

**Web-only (no dotfile support):** ChatGPT, Gemini, Deepseek, Qwen, GLM, Kimi

---

## Quick Reference

| Platform | Injection Method | File |
|----------|-----------------|------|
| Claude | Project Instructions / CLAUDE.md | Web UI / project root |
| ChatGPT | Custom GPT Instructions | Web UI |
| GitHub Copilot | VS Code settings | `.github/copilot-instructions.md` |
| Codex CLI | Auto-load | `AGENTS.md` |
| Gemini | Gems / AI Studio | Web UI |
| Deepseek / Qwen / GLM / Kimi | System message | Web UI / API |
| Cursor | Rules for AI | `.cursor/rules/*.mdc` |
| Windsurf | Cascade Rules | `.windsurf/rules/*.md` |
| Claude Code | Auto-load | `CLAUDE.md` |
| Opencode | System Instructions | Settings |
| Antigravity | AI Rules | Settings / `AGENTS.md` |

---

## Tips

- **Dotfiles take priority** over manual paste — use them for persistent projects
- **Priority order:** editor-native rules > project dotfile > global settings
- **Cross-tool standard:** `AGENTS.md` is emerging as a universal convention across coding agents
- **Verify injection:** ask "What rules are you following?" after setup