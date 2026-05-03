---
name: skill-seekers
description: Converts any documentation website, GitHub repo, API reference, or technical resource into a ready-to-upload Claude skill (SKILL.md file). Use when the user wants to turn documentation into a persistent skill — e.g. "make a skill from the FastAPI docs", "convert the Anthropic API reference into a skill", "I want Claude to know the Supabase docs", "turn this GitHub README into a skill". Analyzes the source, extracts the most useful patterns and procedures, and outputs a complete SKILL.md file.
---

# Skill Seekers — Documentation → Claude Skill Converter

Convert any documentation source into a Claude skill.

## Process

### Step 1 — Analyze the Source
Before writing anything, understand what the source contains:
- What is the primary use case?
- What are the most common tasks a developer would do with this?
- What are the non-obvious patterns / gotchas that aren't in the happy path?
- What does someone need to know that they *can't* easily find by searching?

### Step 2 — Determine Skill Type
Choose the right skill structure based on the source:

| Source Type | Best Skill Structure |
|-------------|---------------------|
| API Reference | Cheat sheet + common patterns |
| Framework docs | Workflow guide + gotchas |
| GitHub README | Quickstart + architecture notes |
| Tutorial | Distilled steps + adaptation notes |
| Design system | Component usage + constraints |

### Step 3 — Extract What Matters
Prioritize:
1. **Patterns** — the idiomatic way to do the most common 20% of tasks
2. **Gotchas** — what breaks, what's counterintuitive, what the docs bury
3. **Configuration** — the parameters/options that actually matter
4. **Examples** — concrete code or step sequences, not conceptual explanations

Do NOT include:
- Comprehensive coverage of every feature (skill context is limited)
- Content that's easily searchable (basic concepts, definitions)
- Installation instructions (one-time, not recurring)

### Step 4 — Write the SKILL.md

Template:
```markdown
---
name: [kebab-case-name]
description: [Third-person trigger description. When to use this skill.
Include key action verbs: "Use when building X", "Use when the user
asks about Y", "Activate when working with Z". Be specific about triggers.]
---

# [Tool/Framework Name] Reference

## Quick Patterns

### [Most common task 1]
[Code example or steps]

### [Most common task 2]
[Code example or steps]

### [Most common task 3]
[Code example or steps]

## Key Concepts
[The 3-5 concepts that unlock everything else. Not a glossary — only what changes behavior.]

## Gotchas & Non-Obvious Behavior
- [Gotcha 1]: [What it is, why it matters, how to handle it]
- [Gotcha 2]: ...
- [Gotcha 3]: ...

## Configuration Reference
[Only the options that actually matter for real usage]

## Common Patterns
[2-3 complete, copy-pasteable examples for typical use cases]

Source: [URL of original documentation]
```

### Step 5 — Validate the Description
The `description` field is the most important part. It determines when Claude loads the skill.

Good description: "Use when building FastAPI applications, defining routes, handling authentication, writing Pydantic models, or when the user asks how to do anything with FastAPI."

Bad description: "A reference skill for FastAPI that contains patterns and examples."

Rules for the description:
- Third person perspective
- List specific trigger conditions
- Include tool name + adjacent concepts users might ask about
- Do NOT summarize the skill's workflow (Claude will follow the description instead of reading the skill)

## Usage

When the user provides a URL or names a documentation source:
1. Fetch and read the documentation (use web search/fetch as needed)
2. Apply the process above
3. Output the complete SKILL.md content
4. Offer to refine based on specific use cases the user has in mind

Source: adapted from yusufkaraaslan/Skill_Seekers concept
