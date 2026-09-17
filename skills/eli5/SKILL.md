---
name: eli5
description: Explain a topic like I'm a 5 year old. Use when the user types /eli5 <topic> or asks for a dead-simple picture explainer of how something works.
---

# eli5

Explain like I'm someone who knows nothing about this topic, using a HTML artifact with big pictures and few words.

Topic: $ARGUMENTS

## Output location

Save to `<project-root>/eli5/<topic>.html` (the directory the user invoked the skill from).

- `<topic>` is a short slug derived from `$ARGUMENTS` (lowercase, dashes for spaces, strip punctuation). Reject empty slugs, `..`, `/`, or punctuation-only — ask the user to rephrase. For CJK topics, keep the raw characters.

Draft (hook → 3–6 step sections → wow line), build the inline SVGs, then write the HTML to this path and show the artifact in the chat (with the file path).
