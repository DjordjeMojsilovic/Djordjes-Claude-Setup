---
name: interactive-learning
description: Create interactive HTML learning tools — flashcard decks, visual theory explainers, and concept pages — for studying. Use this skill whenever the user wants to learn, review, or practice a topic interactively, wants flashcards, a visual summary, a quiz, or says things like "erkläre mir X interaktiv", "mach mir Lernkarten zu X", "ich will X üben", "help me study X", "make a study page for X", or "build me a flashcard deck on X". Covers all subjects including mathematics, statistics, programming, general education (BM/Schule), and quantitative finance/trading. Always prefer this skill over plain text explanations when the user wants to actively learn or review something, not just read about it.
---

# Interactive Learning Skill

Turn any topic into a polished, self-contained HTML learning tool. No frameworks, no dependencies beyond CDN libraries when needed.

## Standard page structure (always follow this order)

Every learning tool MUST have this structure — theory first, interactive second:

1. **Theory Section** (top) — visual explainer with diagrams, annotations, SVG graphics, step-by-step breakdowns
2. **Flashcard / Practice Section** (bottom) — interactive drill after the theory is understood

Never skip the theory section, even if the user only asks for flashcards. The theory anchors the cards.

### When to adjust format

| User intent | Adjustment |
|---|---|
| "Erkläre mir X" | Expand theory heavily, flashcards optional |
| "Lernkarten zu X" | Standard theory + full flashcard deck |
| "Ich will X üben" | Light theory recap + interactive exercises with input fields |

## Design principles

Read `/mnt/skills/public/frontend-design/SKILL.md` for aesthetic guidance. Key points for learning tools specifically:

- **Dark theme preferred** — easier on eyes during long study sessions
- **One topic per screen** — don't overwhelm; use cards, tabs, or steps to chunk information
- **Immediate feedback** — reveal answers, highlight correct/wrong, show worked solutions inline
- **Progress indicators** — card X of Y, completion %, streak counters motivate
- **Mobile-friendly** — learners study on phones; use `max-width: 700px`, large tap targets
- **Keyboard shortcuts** — spacebar to flip card, arrow keys to navigate, enter to confirm answer

## Flashcard Deck — implementation guide

```html
<!-- Core state -->
<script>
const cards = [
  { front: "Was ist CVD?", back: "Cumulative Volume Delta — kumulierte Differenz zwischen Buy- und Sell-Volumen." },
  // ...
];
let current = 0, flipped = false, score = { correct: 0, total: 0 };

function flip() { /* toggle .flipped class */ }
function next(knew) { score.total++; if (knew) score.correct++; current = (current+1) % cards.length; }
</script>

<!-- Card structure -->
<div class="card" onclick="flip()">
  <div class="front">{{ cards[current].front }}</div>
  <div class="back">{{ cards[current].back }}</div>
</div>
<button onclick="next(true)">✓ Wusste ich</button>
<button onclick="next(false)">✗ Nochmal</button>
```

**CSS flip animation:**
```css
.card { perspective: 1000px; cursor: pointer; }
.card-inner { transition: transform 0.5s; transform-style: preserve-3d; }
.card.flipped .card-inner { transform: rotateY(180deg); }
.front, .back { backface-visibility: hidden; position: absolute; width: 100%; }
.back { transform: rotateY(180deg); }
```

## Theory Section — implementation guide

Structure:
1. **Hero** — topic name, one-sentence summary, a "Was du lernen wirst" bullet list
2. **Concept blocks** — each concept: plain-language definition → formal definition → annotated SVG diagram or visual → worked example
3. **Key formulas** — rendered with KaTeX for math/quant topics
4. **Visual types to include (use SVGs inline, no external image deps):**
   - **Flow diagrams** — boxes + arrows showing process steps (e.g. how CVD is computed per trade)
   - **Annotated charts** — simplified price/indicator charts drawn in SVG
   - **Comparison visuals** — side-by-side concept comparisons
   - **Formula breakdowns** — formula rendered in KaTeX with labeled parts below
   - **Timeline / sequence diagrams** — for processes that unfold over time
5. **Sticky section nav** — clicking jumps to each concept block (smooth scroll)

### SVG diagram pattern
```html
<svg viewBox="0 0 600 200" xmlns="http://www.w3.org/2000/svg" style="width:100%;max-width:600px">
  <!-- boxes -->
  <rect x="20" y="70" width="130" height="50" rx="8" fill="#1a1a2e" stroke="#00e5ff" stroke-width="1.5"/>
  <text x="85" y="100" text-anchor="middle" fill="#e0e0f0" font-size="13" font-family="Space Mono">Trade eingeht</text>
  <!-- arrow -->
  <line x1="150" y1="95" x2="200" y2="95" stroke="#6b6b8a" stroke-width="1.5" marker-end="url(#arr)"/>
  <defs>
    <marker id="arr" markerWidth="8" markerHeight="8" refX="6" refY="3" orient="auto">
      <path d="M0,0 L0,6 L8,3 z" fill="#6b6b8a"/>
    </marker>
  </defs>
</svg>
```

For math/stats/quant topics, always use KaTeX:
```html
<link rel="stylesheet" href="https://cdn.jsdelivr.net/npm/katex@0.16.9/dist/katex.min.css">
<script src="https://cdn.jsdelivr.net/npm/katex@0.16.9/dist/katex.min.js"></script>
<script>
  document.querySelectorAll('.math').forEach(el => {
    katex.render(el.textContent, el, { throwOnError: false });
  });
</script>
```

## Subject-specific notes

### Mathe / Statistik
- Always render formulas with KaTeX
- Include worked numerical examples with step-by-step annotations
- Use SVG or canvas for graphs (no external chart libs needed for simple plots)

### Programmierung / Informatik
- Use `<pre><code>` blocks with a dark syntax theme (Monokai palette)
- For algo explanations, animate the steps with JS (highlight current step, show state)

### BM / Allgemeinbildung
- Include Lernziele at the top ("Nach dieser Einheit kannst du…")
- Use real Swiss examples (CHF, Schweizer Recht, etc.) where relevant
- Structure to match Lehrplan-style: Wissen → Verstehen → Anwenden

### Quant Finance / Trading
- Define terms precisely (e.g. CVD = sum of signed delta per trade)
- Include realistic market data examples (fake but plausible prices/volumes)
- Link concepts to practical trading decisions where possible

## Output checklist

Before delivering the artifact:
- [ ] Single self-contained HTML file, no external CSS files
- [ ] Works offline (CDN libs only for math rendering or fonts)
- [ ] Keyboard navigation implemented
- [ ] Mobile layout tested (check at 375px width mentally)
- [ ] Progress/score displayed
- [ ] Aesthetic is distinctive — not default Bootstrap/generic
- [ ] Content is accurate and appropriately detailed for the subject
