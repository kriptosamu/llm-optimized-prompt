# Integration Guide

How to inject the optimized prompt into various LLMs and AI editors.

---

## LLMs

### Claude (Anthropic)
**Projects:**
1. Go to [claude.ai](https://claude.ai) → Settings → Projects
2. Create/select project → "Project Instructions"
3. Paste the prompt

**Direct:**
- Start new chat with prompt as first message (system context)

---

### ChatGPT / GPT-4
**Custom GPTs:**
1. Go to [chat.openai.com](https://chat.openai.com) → Explore GPTs → Create
2. Configure tab → "Instructions" field
3. Paste the prompt

**Temporary:**
- Paste prompt as first message, follow with task

---

### Codex (GitHub Copilot)
1. VS Code → Settings → Copilot → `copilot.instructions`
2. Or create `.github/copilot-instructions.md` in repo
3. Paste prompt content

---

### Gemini (Google)
**Gems:**
1. [gemini.google.com](https://gemini.google.com) → Gem Manager → New Gem
2. "Instructions" field → paste prompt

---

### Deepseek
- Web: Paste prompt as system context in first message
- API: Include in `system` role message

---

### Qwen (Alibaba)
- Web chat: Paste as first message
- API: Use `system` field in request body

---

### GLM (Zhipu AI)
- Web: [chatglm.cn](https://chatglm.cn) → paste as context-setting message
- API: Pass in `system` parameter

---

### Kimi (Moonshot)
- Web: [kimi.moonshot.cn](https://kimi.moonshot.cn)
- Paste prompt first, then task in same or follow-up message

---

## AI Editors

### Cursor
1. Settings (⌘/Ctrl + ,) → General → "Rules for AI"
2. Or create `.cursorrules` file in project root
3. Paste prompt content

**Per-project:** Create `.cursorrules` in repo root

---

### Windsurf
1. Settings → Cascade → "System Prompt" or "Memory"
2. Or create `.windsurf/rules.md`
3. Paste prompt

**Project-specific:** Create `.windsurf/rules.md` in repo

---

### Opencode
1. Settings → AI Configuration → System Instructions
2. Paste prompt into text field
3. Save

---

### Antigravity
1. Project settings → AI Rules
2. Or create `.antigravity/rules` file
3. Paste prompt content

---

## Quick Reference Table

| Platform | Method | File/Location |
|----------|--------|---------------|
| Claude | Project settings | Web UI |
| GPT/Copilot | Custom GPT / Settings | Web UI / `.github/copilot-instructions.md` |
| Codex | VS Code settings | Settings / `.github/copilot-instructions.md` |
| Gemini | Gems | Web UI |
| Deepseek | System message | Web UI / API |
| Qwen | System message | Web UI / API |
| GLM | System parameter | Web UI / API |
| Kimi | First message context | Web UI |
| Cursor | Rules | Settings / `.cursorrules` |
| Windsurf | System Prompt | Settings / `.windsurf/rules.md` |
| Opencode | System Instructions | Settings |
| Antigravity | AI Rules | Settings / `.antigravity/rules` |

---

## Tips

- **File-based injection:** Most editors auto-load rules from dotfiles
- **Priority:** Editor-native rules > project files > global settings
- **Testing:** Verify the prompt took effect by asking "What rules are you following?"
