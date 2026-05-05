# Prompt Tags — Reference Guide

Token cost: L = low, M = medium, H = high
Effect arrows: ↑ = improves, ↓ = reduces, ↑↑ = strong effect

---

## 🟢 Low cost — always safe to use

### `You are an expert [domain]`
```
You are an expert software engineer.
You are an expert data analyst.
```
- Role prompting — activates domain-specific knowledge and vocabulary
- Measurable improvement on domain tasks across multiple benchmarks [CONFIRMED — Zheng et al. 2023, "Large Language Models Are Not Yet Human-Level"]
- Replace `[domain]` with the most specific role relevant to the task
- Token cost: L | Effect: output quality ↑↑, domain accuracy ↑

---

### `silently`
```
Before answering, silently: reason thoroughly.
```
- Instructs the model to reason internally without exposing intermediate steps in output
- Effective at reducing output verbosity while maintaining reasoning quality on standard models
- **Caveat:** On complex multi-step tasks (math, logic chains), suppressing visible reasoning can **degrade accuracy** — the model may lose track of intermediate state without a visible scratchpad [CONFIRMED — LLM reasoning research]
- **Caveat:** Redundant on models with native thinking/reasoning mode (Claude thinking, o1/o3, Gemini thinking) — these models already reason internally via dedicated tokens
- Token cost: L (input) / variable (hidden reasoning) | Effect: output ↓, reasoning ↑ on simple tasks

---

### `No greetings, filler, hedging, or repetition`
- Reduces conversational padding in model output
- "hedging" removes phrases like "it's worth noting that..." or "keep in mind..."
- Estimated impact: meaningful reduction in output tokens, especially for conversational models [approximate — no peer-reviewed quantification of exact percentage]
- Token cost: L | Effect: output ↓↓

---

### `Output: X only`
```
Output: code only.
Output: bullets only.
Output: final text only.
```
- Forces format — reduces output, increases information density
- Token cost: L | Effect: output ↓↓, format ↑

---

### `No explanation unless asked`
- Complements `Output: X only`
- Without this, the model adds explanations even with forced format
- Token cost: L | Effect: output ↓

---

### `Ambiguous? Ask 1 question. Else assume and state it explicitly.`
- Reduces round-trips on clear tasks
- `state it explicitly` is critical — without it, the model assumes **silently**, increasing hallucination risk
- **Risk:** on highly ambiguous tasks, model may still make poor assumptions
- Token cost: L | Effect: interruptions ↓, transparency ↑

---

### `State your assumption explicitly`
- Makes model assumptions visible
- Allows fast correction without re-reading full output
- Token cost: L | Effect: hallucination risk ↓, transparency ↑

---

## 🟡 Medium cost — use with judgment

### `Before answering, silently: identify problem type`
- Forces task categorization before responding
- High impact when approach changes based on problem type
- The cost here is hidden reasoning tokens, not the keyword itself
- Token cost: M (hidden reasoning) | Effect: reasoning ↑↑

---

### `Consider edge cases`
- Reduces errors on boundary inputs, null cases, exceptions
- Especially useful for coding and data analysis
- Token cost: M | Effect: correctness ↑, output quality ↑↑

---

### `Identify root cause before solution`
- Essential for debugging — prevents symptomatic fixes
- Token cost: M | Effect: fix quality ↑↑, output tokens ↑ slightly

---

### `Distinguish fact from inference explicitly`
- Forces the model to mark what is certain vs. deduced
- Reduces hallucinations presented as facts
- Token cost: M | Effect: hallucination risk ↓↓, reliability ↑

---

### `Flag assumptions that materially affect the recommendation`
- Selective version of `State your assumption explicitly`
- Only critical assumptions are surfaced — less noise
- Token cost: M | Effect: hallucination risk ↓, output quality ↑

---

## 🔴 High cost — use only when necessary

### `Think step by step`
- Zero-shot chain-of-thought prompting (Kojima et al., 2022 — "Large Language Models are Zero-Shot Reasoners")
- Related: few-shot chain-of-thought (Wei et al., 2022 — "Chain-of-Thought Prompting Elicits Reasoning in Large Language Models")
- Significantly increases output tokens — exposes full reasoning chain
- Useful only when explicit reasoning is the deliverable or task requires visible scratchpad
- CoT is an emergent ability — benefits are strongest in large models (100B+ parameters) [CONFIRMED — Wei et al., 2022]
- Token cost: H | Effect: reasoning ↑↑↑, output ↑↑↑

---

### `Show your work`
- Variant of step-by-step, common in math/logic contexts
- Same tradeoffs: output explodes, quality increases
- Token cost: H | Effect: reasoning ↑↑↑, output ↑↑↑

---

### Few-shot examples
```
Example input: ...
Example output: ...
```
- Most powerful technique for complex and repetitive tasks
- High input token cost — occupies context window
- Amortized over long sessions or repeated identical tasks
- Token cost: H (input) | Effect: output quality ↑↑↑, format consistency ↑↑↑

---

### `Consider counterarguments`
- Forces alternative perspectives — useful for analysis, strategy, research
- Increases output but reduces bias and rushed conclusions
- Token cost: H | Effect: reasoning quality ↑↑, hallucination risk ↓

---

### `Before answering, identify: [long list]`
```
Before answering, identify: user goal, constraints, edge cases,
failure modes, alternatives, and second-order effects.
```
- Long identifier list = much deeper reasoning
- Internal output explodes — visible only if `silently` is removed
- Token cost: H | Effect: reasoning ↑↑↑

---

## Recommended Combinations

### Maximum efficiency (fewer tokens, solid reasoning)
```
Before answering, silently: identify problem type, consider edge cases.
Output: minimal. No explanation unless asked.
No greetings, filler, hedging, or repetition.
Ambiguous? Ask 1 question. Else assume and state it explicitly.
```

### Maximum quality (more tokens, deep reasoning)
```
Before answering: identify problem type, consider edge cases,
counterarguments, and second-order effects.
Show your work. Flag all assumptions.
Output: structured — use headers and bullets.
```

### Balanced (recommended default)
```
You are an expert [domain].
Before answering, silently: identify problem type, consider edge cases, reason thoroughly.
Output: minimal — [format] only, no explanation unless asked.
No greetings, filler, hedging, or repetition.
Ambiguous? Ask 1 question. Else assume and state it explicitly.
```

---

## Notes

- `silently` is high-efficiency on standard models — but redundant on reasoning models (Claude thinking, o1/o3)
- Few-shot is the most powerful technique but only cost-effective for repetitive tasks
- `Think step by step` produces more output than `silently + identify problem type` — whether quality/token ratio is better depends on task complexity [no benchmark available]
- No tag eliminates hallucination risk — it only reduces it
- All quantitative claims in this file without citations are reasonable heuristics, not peer-reviewed findings
