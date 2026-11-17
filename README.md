# AI tools tracker — token optimisation and LLM cost reduction (2026)

A documentation-only comparison of tools that reduce LLM token consumption, latency or cost:
prompt compression, model routing, native and semantic caching, KV-cache pruning, budgeting and
observability. It is written for developers choosing a cost-reduction stack and produces no code
or data — the output is the three Markdown documents in this repository.

> Status: archived snapshot (last content update 2026-08-11). Figures are taken from vendor
> documentation and published benchmarks as of that date; tools change quickly, so verify any
> number against the current source before relying on it. Not a benchmark we ran ourselves.

> **New here?** See [How to use this repo with AI (Claude, Gemini, ChatGPT)](HOW_TO_USE_WITH_AI.md).

## What it does
- Summarises 20+ tools across seven categories: compression, budgeting, retrieval/context pruning,
  caching and batching, model routing, KV-cache / inference optimisation, observability.
- Gives a one-table quick comparison (savings claim, setup time, maturity) for the headline tools.
- Sketches the 2026 market landscape as four "lanes" (gateways, routers, observability/caching,
  endpoint optimisers) with representative products per lane.
- Recommends a starting stack for four use cases (solo dev, multi-model enterprise, multi-repo
  research, production RAG) in `docs/GETTING_STARTED.md`.
- Compares the author's own "Token Optimizer" workflow against LLMLingua-2, RouteLLM, prompt
  caching, semantic caching and Provence in `docs/COMPETITIVE_ANALYSIS.md`.

## Quick start
There is nothing to install or run. Read in this order:

1. The comparison tables below.
2. [`docs/GETTING_STARTED.md`](docs/GETTING_STARTED.md) — pick a first tool in five minutes.
3. [`docs/COMPETITIVE_ANALYSIS.md`](docs/COMPETITIVE_ANALYSIS.md) — performance matrix, feature gaps, sustainability take.

```bash
git clone https://github.com/herrrickshaw/ai-tools-tracker.git
cd ai-tools-tracker
```

## Quick comparison

| Tool | Category | Claimed savings | Setup | Maturity |
|------|----------|-----------------|-------|----------|
| Anthropic Prompt Caching | Native caching | 90% on cached inputs | 0 min | Production |
| LLMLingua-2 | Compression | 80–95% | 5 min | Production |
| RouteLLM | Model routing | 50–85% | 30 min | Production |
| Semantic caching (Bifrost, GPTCache) | Query caching | 20–45% on hits | 2–4 h | Production |
| SlimInfer | KV-cache pruning | 66x memory reduction | 10 min | Research |
| Token Optimizer (author's own) | Multi-repo + budget | 55–75% | 15 min | Personal use |

## Tools by category

| Category | Tools covered |
|---|---|
| 1. Prompt compression (20–95x) | LLMLingua-2 (question-aware, 80–95%), LLMLingua (original, 20x), Token Optimizer markitdown conversion (40–60%) |
| 2. Token budgeting and tracking | Tokencap (SDK-level hard budget), ContextOps (pre-call optimisation + PII scan), Token Optimizer budget tracker |
| 3. Retrieval and context optimisation (40–50%) | Provence (evidence-aware pruning for RAG), SlimRAG (entity-aware selection), Token Optimizer graphify ranking |
| 4. Caching and batching (50–90%) | Anthropic prompt caching (90%), semantic caching — Bifrost, GPTCache, Redis Stack (20–45% hits), batch APIs (50% cost) |
| 5. Model routing (50–85%) | RouteLLM (LMSYS, 85%), LiteLLM, OpenRouter, Portkey |
| 6. KV cache and inference | SlimInfer (dynamic token pruning, 66x), contextual pruning (MIT) |
| 7. Observability and cost tracking | Langfuse, Braintrust, Bifrost (4-tier spend hierarchy, 11 µs overhead), Datadog LLM |

The earlier README linked a `tools/<category>/<tool>.md` page per tool. Those pages were never
committed; the per-tool detail lives in the two `docs/` files instead.

## Market landscape (2026)

```
Lane 1: AI gateways          Portkey · LiteLLM · Helicone · Kong
Lane 2: Intelligent routers  RouteLLM (LMSYS) · OpenRouter · Not Diamond · custom routers
Lane 3: Observability/cache  Langfuse · Bifrost · GPTCache · Redis Stack
Lane 4: Endpoint optimisers  SlimInfer · Contextual Pruning · Token Optimizer (multi-repo)
```

| Strategy | Typical savings | Implementation cost |
|----------|-----------------|---------------------|
| Prompt caching (native) | 90% (cached) | $0 |
| Semantic caching | 20–45% (hits) | $500–2k |
| Model routing | 50–85% | $1–5k |
| Compression | 20–95% | $0–1k |
| KV-cache pruning | 50–66x memory | $0–500 |
| Combined (all layers) | 55–93% | $2–10k |

## Choosing a stack

| Use case | Recommended combination | Claimed savings | Setup | Cost |
|---|---|---|---|---|
| Cost-conscious solo dev | Anthropic caching + semantic caching + budget tracker | 60–75% | 2 h | $0 |
| Multi-model enterprise | RouteLLM + Langfuse + semantic caching | 65–85% | 1–2 days | $5–15k/yr |
| Multi-repo research | Token Optimizer + LLMLingua-2 + semantic caching | 70–82% | 1 day | $0–500 |
| Production RAG | Provence + semantic caching + model routing | 60–75% | 2–3 days | $2–5k/yr |

## Repository layout
| Path | Purpose |
|---|---|
| `README.md` | This overview and the comparison tables |
| `docs/GETTING_STARTED.md` | Self-assessment, four recommended stacks, step-by-step for the solo-dev stack, validation snippets |
| `docs/COMPETITIVE_ANALYSIS.md` | Performance matrix, category winners, strengths/weaknesses, feature-gap and sustainability analysis |
| `HOW_TO_USE_WITH_AI.md` | How a non-programmer can hand this repo to an AI assistant |
| `CLAUDE.md` | Guidance for Claude Code sessions (source-fetching rules) |
| `graphify-out/` | Generated knowledge-graph cache of the Markdown files; not hand-edited |
| `.github/workflows/quality-gates.yml` | gitleaks secret scan on push / PR |

## Data sources
Figures are compiled, not measured here, from:

| Source | What is taken |
|---|---|
| Published benchmarks (AAAI 2026, NeurIPS 2025) | SlimInfer and compression results |
| Vendor documentation (Anthropic, OpenAI, Together AI) | Caching, batch-API and pricing claims |
| Open-source project pages (LLMLingua, vLLM, LiteLLM, RouteLLM) | Setup effort, feature lists |
| Author's own Token Optimizer usage | The 55–75% "personal use" figure — self-reported, not externally validated |

## Limitations and known issues
- Snapshot dated 2026-08-11; nothing has been re-verified since.
- All savings percentages are vendor or paper claims under their own workloads, not a common benchmark.
- The "Token Optimizer" rows describe the author's private workflow (scripts under `~/.claude/scripts/`
  in another repository); they are not installable from this repo.
- `docs/GETTING_STARTED.md` references `claude-3-5-sonnet-20241022`, which is an older model ID.
- The earlier README promised `docs/BENCHMARKS.md`, `docs/INTEGRATION_PATTERNS.md`,
  `docs/VENDOR_COMPARISON.md`, `docs/COST_CALCULATOR.md` and `CONTRIBUTING.md`; none exist.

## Related repositories
- [`global-market-research-platform`](https://github.com/herrrickshaw/global-market-research-platform/tree/token-optimizer) — the `token-optimizer` branch that the "Token Optimizer" entries refer to.

## Licence
The previous README declared MIT, but no `LICENSE` file is committed, so the licence is not yet
binding. Adding a `LICENSE` file is the intended next step.
