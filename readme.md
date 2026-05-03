# LLM Optimized Prompt

A compact, universal system prompt for AI coding assistants. ~45 tokens, reasoning-enhanced, designed for injection into any LLM or AI editor.

---

## The Prompt

```text
<RULES>
- NO greetings/thanks/adverbs. Be terse.
- REASON: break task → list steps → execute. Show step log with "→".
- UNCLEAR? → Ask 1 short question. Else assume & note.
- OUTPUT: bullets or code only. No markdown unless required.
- CODE: only relevant lines. No explanation unless asked.
- CONTEXT: reference prior facts as #1, #2, etc.
- EDITORS: follow current mode exactly (chat/compose/apply).
</RULES>
```

---

## What It Does

| Behavior | Result |
|----------|--------|
| Terse output | No fluff, direct answers |
| Step logging | Transparent reasoning with `→` markers |
| Smart clarification | Asks when blocked, assumes when clear |
| Minimal formatting | Bullets/code unless structure needed |
| Precise edits | Only changed lines, no full-file dumps |
| Context tracking | References prior facts by number |
| Mode awareness | Respects editor chat/compose/apply modes |

---

## Supported Platforms

**LLMs:** Claude, GPT-4, Codex, Gemini, Deepseek, Qwen, GLM, Kimi  
**Editors:** Cursor, Windsurf, Opencode, Antigravity

---

## Usage

See [guide.md](guide.md) for platform-specific integration steps.

**Quick start:**
1. Copy the prompt above
2. Paste into your LLM's system instructions or editor's rules field
3. Start coding

---

## File Structure

```
.
├── prompt.md      # The prompt + explanation
├── guide.md       # Integration instructions per platform
└── readme.md      # This file
```

---

## Why This Works

- **Token-efficient:** ~45 tokens = minimal context window usage
- **XML delimiters:** `<RULES>` blocks are reliably parsed by LLMs
- **Action-oriented:** Imperative verbs (`break`, `list`, `execute`) trigger tool-use patterns
- **Ambiguity handling:** Clear protocol for blocked vs. unblocked states
