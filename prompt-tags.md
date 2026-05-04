# Prompt Tags — Reference Guide

Token cost: L = low, M = medium, H = high

---

## 🟢 Low cost — always safe to use

### `silently`
```
Before answering, silently: reason thoroughly.
```
- Activates internal reasoning without showing it in output
- Load-bearing: removing it increases output by 2-5x
- Token cost: L | Effect: reasoning ↑, output ↓

---

### `No greetings, filler, hedging, or repetition`
- Cuts ~20-40% of output tokens on average
- "hedging" removes phrases like "it's worth noting that..." or "keep in mind..."
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

### `Ambiguous? Ask 1 question. Else assume and proceed.`
- Reduces round-trips on clear tasks
- **Risk:** on ambiguous tasks, model may hallucinate silently
- Mitigation: add `State your assumption explicitly`
- Token cost: L | Effect: interruptions ↓, hallucination risk ↑

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
- Most studied technique in literature (Wei et al., 2022)
- Significantly increases output tokens — exposes full reasoning
- Useful only when explicit reasoning is the deliverable
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

- `silently` is the most efficient tag — maximum impact, zero cost
- Few-shot is the most powerful but should only be used for repetitive tasks
- `Think step by step` is outperformed by `silently + identify problem type` in quality/token ratio
- No tag eliminates hallucination risk — it only reduces it
