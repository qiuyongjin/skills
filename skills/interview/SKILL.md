---
name: interview
description: Answer a question from the interviewee's perspective with a clear, well-structured HTML artifact. Use when the user types /interview <question> or asks for an interview-style answer.
---

# interview

Answer $ARGUMENTS as a job candidate would in an interview. Produce a HTML artifact with a clear structure, confident tone, and no filler.

Question: $ARGUMENTS

## Output location

Save to `<project-root>/interview/<question-slug>.html` (the directory the user invoked the skill from). Use a kebab-case slug of the question (first ~6 words, lowercase, no punctuation).

## Structure

Pick the pattern that fits the question type:

**Technical / conceptual** — "What is X?", "How does Y work?":
1. One-line direct answer
2. 2–3 labeled sections (e.g. **Core idea**, **How it works**, **Trade-offs**)
3. Short example if helpful

**Behavioral** — "Tell me about a time...", "How would you handle...":
1. One-line framing (what you did / would do)
2. STAR as 2–4 short bullets: **Situation**, **Task**, **Action**, **Result**
3. What you learned (optional, 1 sentence)

**Opinion / open-ended** — "Why...", "What's your view on...":
1. Thesis statement (1–2 sentences)
2. 2–3 supporting reasons
3. Counterpoint or nuance (optional)
4. Conclusion (1 sentence)

## Tone

- Confident and direct; no hedging
- First person ("I would...", "In my experience...") for behavioral questions
- Direct statements for factual / technical questions
- No filler ("Great question", "I think that", "It's important to note")
- Each section ≤ 3 short sentences
