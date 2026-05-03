---
name: cookbook
description: Use this skill whenever the user is building something with the Claude API and would benefit from a known-good reference implementation from Anthropic's official Claude Cookbooks. Trigger on any request that touches Claude API features — RAG, tool use, agents (Agent SDK or Managed Agents), vision/multimodal, prompt caching, batch processing, extended thinking, citations, JSON mode, message batches, finetuning, evals, skills, memory, parallel tools, structured output, sub-agents — or on integrations (Pinecone, MongoDB, LlamaIndex, Wikipedia, Wolfram, ElevenLabs, Deepgram, VoyageAI). Trigger even when the user doesn't explicitly say "cookbook": questions like "how do I do X with Claude", "what's the recommended pattern for Y", "show me how to build Z with the Anthropic API", "I want to add tool use to my app", or "best way to handle long contexts" should pull this skill. Do NOT trigger for unrelated coding questions, Claude.ai UI questions, or pure prompting questions that don't involve the API.
---

# Claude Cookbooks Index

The Claude Cookbooks are Anthropic's official collection of reference implementations for building with the Claude API. There are 76 recipes covering nearly every part of the API surface. This skill is an index — when the user asks how to build something with Claude, find the relevant recipe(s) here and point them to the source.

**Repository:** `https://github.com/anthropics/anthropic-cookbook` (also referenced as `claude-cookbooks`)

## How to use this skill

1. Identify what the user is trying to build (RAG? Tool use? Agent? Vision? etc.)
2. Look up the relevant recipe(s) in the index below
3. For deep details on a category, read the matching file in `references/`
4. Recommend the recipe(s) with a one-line summary and the GitHub URL
5. If the user wants the actual code walked through, fetch the notebook URL with web_fetch — don't reconstruct it from memory

The point is to save the user from reinventing patterns Anthropic has already published. Even if you could write the code from scratch, pointing to the canonical recipe is better: the user gets battle-tested code, ongoing maintenance, and links to related patterns.

## Quick category map

If the user's task touches…

| Topic | Read | Top recipes |
|---|---|---|
| Building autonomous agents | `references/agents.md` | Agent SDK series, Managed Agents tutorials, basic workflow patterns |
| Tool use, function calling, structured output | `references/tool_use.md` | Calculator, customer service, parallel tools, PTC, memory cookbook |
| RAG, embeddings, document Q&A, summarization | `references/rag.md` | Contextual retrieval, RAG guide, summarization, citations |
| Vision, images, PDFs, charts, transcription | `references/multimodal.md` | Vision best practices, transcribe, charts/graphs, crop tool |
| API features (caching, batches, JSON, thinking) | `references/responses.md` | Prompt caching, batches, JSON mode, extended thinking |
| Third-party integrations | `references/integrations.md` | Pinecone, MongoDB, LlamaIndex, ElevenLabs, Wolfram |
| Anthropic Skills, evaluation, fine-tuning | `references/skills_and_evals.md` | Building evals, custom skills, finetuning on Bedrock |

## Most-cited recipes (start here when in doubt)

These are the recipes that come up most often. If the user's question fits one of these, recommend it directly — no need to load a reference file first.

**Agents**
- *The chief of staff agent* — multi-agent orchestration with the Claude Agent SDK, subagents, hooks, plan mode → `claude_agent_sdk/01_The_chief_of_staff_agent.ipynb`
- *Build a data analyst agent with Managed Agents* — turn a CSV into an HTML report in a sandbox → `managed_agents/data_analyst_agent.ipynb`
- *Basic workflows* — three foundational multi-LLM patterns (chained, routing, parallelization) → `patterns/agents/basic_workflows.ipynb`
- *Orchestrator workers* — central LLM delegates to worker LLMs and synthesizes results → `patterns/agents/orchestrator_workers.ipynb`

**Tool use**
- *Customer service agent with client-side tools* — the canonical end-to-end tool use example → `tool_use/customer_service_agent.ipynb`
- *Memory & context management with Sonnet 4.6* — persistent memory tool + context editing → `tool_use/memory_cookbook.ipynb`
- *Programmatic tool calling (PTC)* — let Claude write code that calls tools, cuts latency and tokens → `tool_use/programmatic_tool_calling_ptc.ipynb`
- *Tool search with embeddings* — scale past hundreds of tools by retrieving them semantically → `tool_use/tool_search_with_embeddings.ipynb`
- *Extracting structured JSON using tool use* — most reliable way to get structured output → `tool_use/extracting_structured_json.ipynb`

**RAG & retrieval**
- *Enhancing RAG with contextual retrieval* — the contextual embeddings technique that made big accuracy gains → `capabilities/contextual-embeddings/guide.ipynb`
- *Retrieval augmented generation* — the main RAG guide with summary indexing and reranking → `capabilities/retrieval_augmented_generation/guide.ipynb`
- *Citations* — make Claude cite its sources when answering from documents → `misc/using_citations.ipynb`

**Multimodal**
- *Best practices for using vision with Claude* — start here for any image/vision task → `multimodal/best_practices_for_vision.ipynb`
- *How to transcribe documents with Claude* — extract structured text from images and PDFs → `multimodal/how_to_transcribe_text.ipynb`

**API features**
- *Prompt caching* — cache static prefixes for cost and latency wins, the single highest-leverage feature for most apps → `misc/prompt_caching.ipynb`
- *Batch processing with Message Batches API* — 50% cheaper async processing → `misc/batch_processing.ipynb`
- *Extended thinking* — Claude's transparent reasoning mode with budget control → `extended_thinking/extended_thinking.ipynb`

## How to construct GitHub URLs

All recipe paths are relative to the repository root. To get a clickable URL, prepend `https://github.com/anthropics/anthropic-cookbook/blob/main/` to the path. For example, `tool_use/calculator_tool.ipynb` becomes `https://github.com/anthropics/anthropic-cookbook/blob/main/tool_use/calculator_tool.ipynb`.

If the user wants to read the actual notebook content (not just the description), fetch this URL with `web_fetch` — it returns the rendered notebook with code and outputs.

## Recipe categories at a glance

By category count, the cookbook breaks down roughly:

- **Tools** (11) — function calling, structured output, parallel calls, memory, context management
- **Agent Patterns** (11) — multi-agent workflows, orchestration, sub-agents
- **Integrations** (13) — third-party (Pinecone, MongoDB, LlamaIndex, etc.) and partner integrations
- **Responses** (10) — JSON mode, caching, batches, citations, thinking, frontend output
- **RAG & Retrieval** (9) — embeddings, classification, summarization, knowledge graphs
- **Claude Agent SDK** (6) — the SDK tutorial series
- **Multimodal** (6) — vision, transcription, charts, sub-agents
- **Skills** (3) — intro, financial applications, custom skill development
- **Evals** (3) — building evals, generating test cases, tool evaluation
- **Thinking** (2) — extended thinking with and without tools
- **Observability** (1) — usage and cost Admin API
- **Fine-Tuning** (1) — Haiku on Bedrock

For the full list within any category, read the corresponding file in `references/`.

## When to read a reference file

Read a reference file when:
- The user's question fits a category (e.g., "how do I do RAG?") and you want to scan all the relevant recipes before recommending one
- The user explicitly wants to know "what's available for X"
- You're not sure which recipe in a category is the best fit and want to compare descriptions

Skip the reference files when the answer is one of the most-cited recipes above and the user's question is clear — recommend it directly.

## Things to keep in mind when recommending recipes

- **Match the recipe to the use case, not the keyword.** A user asking "how do I get JSON from Claude?" might be best served by *Extracting structured JSON using tool use* (`tool_use/extracting_structured_json.ipynb`), not the older *Prompting Claude for JSON mode* recipe — tool use is the more reliable path now.
- **Some recipes are dated.** A few date back to 2023 (Claude 2 era). Mention the publication date if it's pre-2024 so the user knows to check whether the API surface has evolved. The Wikipedia search cookbook is one such legacy recipe.
- **Combine recipes where it makes sense.** Real apps usually mix patterns: prompt caching + tool use + structured JSON, or RAG + citations + extended thinking. Don't pretend one recipe covers everything — flag the relevant recipes for each piece.
- **Models in the recipes may be older.** The cookbook uses model aliases like `claude-sonnet-4-6`, `claude-haiku-4-5`, `claude-opus-4-6`. Don't blindly copy a dated model ID from an older notebook into the user's code.
- **The repo is updated continuously.** New recipes get added regularly. If the user asks about something that doesn't appear in this index, suggest they search the repo directly — it may have been added after this skill was last updated.
