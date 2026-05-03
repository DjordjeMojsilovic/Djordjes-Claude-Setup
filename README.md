<div align="center">

# ⚡ Djordje's Claude Setup

**My personal Claude configuration – skills, CLAUDE.md and a complete prompting guide.**

[![Claude](https://img.shields.io/badge/Claude-Sonnet%204.5-blueviolet?style=for-the-badge)](https://claude.ai)
[![Skills](https://img.shields.io/badge/Skills-11-orange?style=for-the-badge)]()
[![License: MIT](https://img.shields.io/badge/License-MIT-blue.svg?style=for-the-badge)](LICENSE)

[![Vibe Coding](https://img.shields.io/badge/Workflow-Vibe%20Coding-ff69b4?style=flat-square)]()
[![Multi Agent](https://img.shields.io/badge/Multi--Agent-Enabled-green?style=flat-square)]()
[![Claude Code](https://img.shields.io/badge/Claude%20Code-Ready-blueviolet?style=flat-square)]()

*Stop chatting with AI. Start working with it.*

</div>

---

## What's in here?

This repo contains my complete Claude setup – the same configuration I use daily for coding, learning, decision-making and research. Everything is plug-and-play: download a skill, upload it to Claude, and it immediately changes how Claude responds.

| File/Folder | Description |
|---|---|
| `CLAUDE.md` | My global Claude Code configuration – rules Claude follows in every session |
| `skills/` | 11 custom skills that extend Claude's capabilities |
| `README.md` | This file – including a full prompting guide |

---

## 🧠 Skills

Skills are `.md` files you upload to Claude via [claude.ai/settings/skills](https://claude.ai/settings/skills). Once uploaded, Claude reads them automatically when relevant and adjusts its behavior accordingly.

### How to install a skill

1. Download the `SKILL.md` file from any folder in `skills/`
2. Go to [claude.ai](https://claude.ai) → Settings → Skills
3. Upload the file
4. Done – Claude will now use it automatically when triggered

---

### Skill Overview

| Skill | What it does | Trigger words |
|---|---|---|
| **ultraplan** | Military-grade analysis before answering – research, assess, plan, execute | `/ultraplan`, "make a plan", "deep dive" |
| **council** | Convenes 7 expert AI personas to debate your decision and give a verdict | "should I...", "convene the council", "stress-test this" |
| **balanced** | Replaces sycophantic responses with structured critical analysis | "challenge this", "is this right?", "steelman this" |
| **decision-toolkit** | RICE scoring, decision matrices, pre-mortem analysis for complex choices | "how should I decide", "prioritize these", "build vs buy" |
| **frontend-design** | Production-grade UI with high design quality – avoids generic AI aesthetics | "build a component", "design a UI", "make a landing page" |
| **ui-ux-pro-max** | 50+ styles, 161 palettes, 57 font pairings across 10 stacks | "design a dashboard", "glassmorphism card", "color palette" |
| **interactive-learning** | Flashcard decks, visual explainers, quizzes for any topic | "make flashcards for X", "help me study X", "explain X interactively" |
| **software-architecture** | Clean Architecture, SOLID, design patterns, anti-patterns | "how should I structure this", "which pattern", "review my architecture" |
| **cookbook** | Official Anthropic patterns for Claude API – RAG, tool use, agents, evals | "how do I do X with Claude API", "show me tool use", "batch processing" |
| **skill-seekers** | Turns any docs, GitHub repo or API reference into a ready-to-upload skill | "make a skill from the FastAPI docs", "convert this README into a skill" |
| **rugpull-detector** | Analyzes crypto tokens for rugpull risk with a 0–100 score | "is X a scam?", "analyze this coin", "rugpull score for X" |

---

## ⚙️ CLAUDE.md

The `CLAUDE.md` file lives in the root of a project and tells Claude Code how to behave in every session. Think of it as a standing instruction set that never needs to be repeated.

```markdown
## Approach
- Think before acting. Read existing files before writing code.
- Be concise in output but thorough in reasoning.
- Prefer editing over rewriting whole files.
- Do not re-read files you have already read unless the file may have changed.
- Skip files over 100KB unless explicitly required.
- Suggest running /cost when a session is running long to monitor cache ratio.
- Recommend starting a new session when switching to an unrelated task.
- Test your code before declaring done.
- No sycophantic openers or closing fluff.
- Keep solutions simple and direct.
- User instructions always override this file.
```

Place this file in the root of any project where you use Claude Code. It applies automatically.

---

## 📖 Prompting Guide

Most people use Claude like a search engine – ask a question, get an answer, move on. That's leaving 80% of the value on the table. Here's how I actually work with Claude.

---

### 1. Give Claude a role before the task

The single most impactful thing you can do. Claude performs dramatically better when it knows who it's supposed to be.

**Bad:**
```
Write me a business plan for a SaaS app.
```

**Good:**
```
You are a senior product strategist with 10 years experience launching B2B SaaS products 
in the Swiss market. I'm 15 years old and starting my first startup. 
Write me a lean business plan for a no-code AI orchestration tool targeting SMEs.
```

The role defines the lens. The context defines the relevance. Both matter.

---

### 2. Use XML tags for complex inputs

When you give Claude multiple pieces of information, structure them with tags. It dramatically reduces confusion and hallucination.

```
<task>Review this code and find bugs</task>

<context>
This is an ESP32-S3 Arduino sketch running FreeRTOS dual-core.
The bug causes a heap crash after 5 AI requests.
</context>

<code>
// paste your code here
</code>

<output_format>
List each bug with: location, root cause, fix
</output_format>
```

---

### 3. Specify the output format explicitly

Claude defaults to whatever format it thinks is appropriate. If you want something specific, ask for it.

```
Respond only in JSON. No markdown, no preamble, no explanation outside the JSON block.

Format:
{
  "verdict": "...",
  "confidence": 0-100,
  "reasons": ["...", "..."],
  "next_steps": ["...", "..."]
}
```

---

### 4. Use skills for recurring tasks

Instead of writing a long system prompt every time, turn it into a skill. Upload it once, use it forever.

Example: Instead of writing *"analyze this token for rugpull risk, give a score from 0-100, check liquidity, ownership concentration, contract audit..."* every single time – that's what the `rugpull-detector` skill does automatically.

**How to create your own skill:**
1. Use the `skill-seekers` skill: *"make a skill from [documentation URL]"*
2. Or write a SKILL.md manually with: name, description, trigger conditions, instructions, output format
3. Upload to Claude → done

---

### 5. Multi-agent workflows (advanced)

Instead of one long conversation, use multiple specialized Claude instances in parallel:

```
Agent 1 (Researcher):   "Research the top 5 competitors of X. Output JSON."
Agent 2 (Analyst):      "Given this competitor data [paste], find gaps. Output JSON."  
Agent 3 (Strategist):   "Given these gaps [paste], write a positioning strategy."
```

Each agent does one job well. The output of one feeds the next. This is how I built the AssistantHub Pro – different Claude sessions for architecture, debugging, UI design and documentation.

---

### 6. The prompts I use most

**For coding:**
```
You are a senior [language] engineer. I'll describe a bug. 
Think step by step before suggesting a fix. 
Show only the changed lines, not the entire file.
Bug: [description]
```

**For decisions:**
```
/ultraplan [decision I need to make]
```

**For critical feedback:**
```
Challenge this idea. Don't validate it – find the weaknesses, 
the edge cases, and the assumptions I'm making that might be wrong.
Idea: [your idea]
```

**For learning:**
```
Make me an interactive flashcard deck on [topic] 
that I can use to study for my exam next week.
```

**For architecture:**
```
Review this system design. Apply Clean Architecture principles. 
List violations and suggest concrete refactors.
[paste your design]
```

---

### 7. What not to do

| ❌ Don't | ✅ Do instead |
|---|---|
| Ask vague questions | Give context, role, constraints |
| Keep one session going forever | Start new sessions per task |
| Accept the first answer blindly | Challenge it: "What are the weaknesses of this?" |
| Paste huge files | Reference specific sections |
| Ask Claude to do everything | Break it into specialized sub-tasks |
| Ignore CLAUDE.md | Put your standing rules in it so you never repeat yourself |

---

## 🗂️ Repository Structure

```
djordjes-claude-setup/
├── CLAUDE.md                    ← Claude Code global config
├── README.md                    ← This file
└── skills/
    ├── balanced/SKILL.md        ← Critical analysis mode
    ├── cookbook/SKILL.md        ← Claude API patterns
    ├── council/SKILL.md         ← 7-expert debate system
    ├── decision-toolkit/SKILL.md← Decision frameworks
    ├── frontend-design/SKILL.md ← Production UI generation
    ├── interactive-learning/SKILL.md ← Flashcards & study tools
    ├── rugpull-detector/SKILL.md← Crypto risk analysis
    ├── skill-seekers/SKILL.md   ← Turn docs into skills
    ├── software-architecture/SKILL.md ← Clean Architecture
    ├── ui-ux-pro-max/SKILL.md   ← Full UI/UX intelligence
    └── ultraplan/SKILL.md       ← Military-grade planning
```

---

## 📄 License

MIT License – free to use, fork and adapt.

---

<div align="center">

Built by **[Djordje Mojsilovic](https://github.com/DjordjeMojsilovic)** | 2026

[![GitHub](https://img.shields.io/badge/GitHub-DjordjeMojsilovic-181717?style=flat-square&logo=github)](https://github.com/DjordjeMojsilovic)
[![AssistantHub Pro](https://img.shields.io/badge/Also%20check%20out-AssistantHub%20Pro-orange?style=flat-square)](https://github.com/DjordjeMojsilovic/AssistantHub-Pro)

*If this helps you work better with Claude – a ⭐ means a lot!*

</div>
