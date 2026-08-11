# AI Tools Tracker 🤖

Comprehensive tracker and comparison of AI tools for **token optimization**, **cost reduction**, and **LLM efficiency** (2026).

> **Focus**: Production-ready tools that demonstrably reduce token consumption, latency, or cost. Not academic papers or vaporware.

---

## 📊 Quick Comparison

| Tool | Category | Savings | Setup | Maturity |
|------|----------|---------|-------|----------|
| **Anthropic Prompt Caching** | Native Caching | 90% (cached inputs) | 0 min | ✅ Production |
| **LLMLingua-2** | Compression | 80-95% | 5 min | ✅ Production |
| **RouteLLM** | Model Routing | 50-85% | 30 min | ✅ Production |
| **Semantic Caching** (Bifrost, GPTCache) | Query Caching | 20-45% (hits) | 2-4 hours | ✅ Production |
| **SlimInfer** | KV Cache Pruning | 66x memory reduction | 10 min | 🔬 Research |
| **Token Optimizer** (our system) | Multi-Repo + Budget | 55-75% | 15 min | ✅ Personal use |

---

## 🏆 Tools by Category

### 1. Prompt Compression (20-95x)
Reduce context size while preserving meaning.

- **[LLMLingua-2](tools/compression/llmlingua2.md)** — Question-aware compression; 80-95% reduction
- **[LLMLingua](tools/compression/llmlingua.md)** — Original (slower); 20x compression
- **[Token Optimizer - Markitdown](tools/compression/token-optimizer.md)** — File format conversion; 40-60%

### 2. Token Budgeting & Tracking
Monitor and enforce token spend limits.

- **[Tokencap](tools/budgeting/tokencap.md)** — Hard budget enforcement at SDK level
- **[ContextOps](tools/budgeting/contextops.md)** — Pre-call optimization + PII scanning
- **[Token Optimizer - Budget Tracker](tools/budgeting/token-optimizer.md)** — Per-session + per-repo tracking

### 3. Retrieval & Context Optimization (40-50%)
Reduce context needed per query.

- **[Provence](tools/retrieval/provence.md)** — Evidence-aware context pruning for RAG
- **[SlimRAG](tools/retrieval/slimrag.md)** — Entity-aware context selection
- **[Token Optimizer - Graphify Integration](tools/retrieval/token-optimizer.md)** — Knowledge-graph ranking

### 4. Caching & Batching (50-90%)
Avoid redundant API calls.

- **[Anthropic Prompt Caching](tools/caching/prompt-caching.md)** — Native API caching; 90% reduction
- **[Semantic Caching](tools/caching/semantic-caching.md)** — Query deduplication; 20-45% hits
  - Bifrost
  - GPTCache
  - Redis Stack
- **[Batch Processing](tools/caching/batch-processing.md)** — Async batch API; 50% cost reduction

### 5. Model Routing (50-85%)
Select cheapest model for task.

- **[RouteLLM](tools/routing/routellm.md)** — Semantic-aware LLM-based routing; 85% savings
- **[LiteLLM](tools/routing/litellm.md)** — Open-source gateway; multi-model support
- **[OpenRouter](tools/routing/openrouter.md)** — Unified API + routing
- **[Portkey](tools/routing/portkey.md)** — Enterprise gateway + observability

### 6. KV Cache & Inference Optimization
Reduce memory and latency.

- **[SlimInfer](tools/inference/sliminfer.md)** — Dynamic token pruning; 66x KV cache reduction
- **[Contextual Pruning](tools/inference/contextual-pruning.md)** — MIT-based architecture pruning

### 7. Observability & Cost Tracking
Monitor spending across all tools.

- **[Langfuse](tools/observability/langfuse.md)** — Open-source; request logs + budget gates
- **[Braintrust](tools/observability/braintrust.md)** — Multi-library tracking + experiments
- **[Bifrost](tools/observability/bifrost.md)** — 4-tier spend hierarchy; 11µs overhead
- **[Datadog LLM](tools/observability/datadog-llm.md)** — Enterprise auto-instrumentation

---

## 📈 Market Landscape (2026)

### Four Lanes of Innovation

```
Lane 1: AI Gateways
├─ Portkey
├─ LiteLLM
├─ Helicone
└─ Kong

Lane 2: Intelligent Routers
├─ RouteLLM (LMSYS)
├─ OpenRouter
├─ Not Diamond
└─ Your custom router

Lane 3: Observability & Caching
├─ Langfuse
├─ Bifrost
├─ GPTCache
└─ Redis Stack

Lane 4: Endpoint Optimizers
├─ SlimInfer
├─ Contextual Pruning
└─ Token Optimizer (multi-repo focus)
```

### Economics (2026)

| Strategy | Typical Savings | Implementation Cost | ROI |
|----------|-----------------|----------------------|-----|
| Prompt caching (native) | 90% (cached) | $0 | ⭐⭐⭐⭐⭐ |
| Semantic caching | 20-45% (hits) | $500-2k | ⭐⭐⭐⭐ |
| Model routing | 50-85% | $1-5k | ⭐⭐⭐⭐ |
| Compression | 20-95% | $0-1k | ⭐⭐⭐⭐ |
| KV cache pruning | 50-66x memory | $0-500 | ⭐⭐⭐ |
| Combined (all layers) | **55-93%** | **$2-10k** | ⭐⭐⭐⭐⭐ |

---

## 🎯 Choosing Your Stack

### Use Case: Cost-Conscious Solo Dev
**Recommendation**: Anthropic Caching + Semantic Caching + Budget Tracker  
**Savings**: 60-75% | **Setup**: 2 hours | **Cost**: $0

### Use Case: Multi-Model Enterprise
**Recommendation**: RouteLLM + Langfuse + Semantic Caching  
**Savings**: 65-85% | **Setup**: 1-2 days | **Cost**: $5-15k/year

### Use Case: Multi-Repo Research
**Recommendation**: Token Optimizer + LLMLingua-2 + Semantic Caching  
**Savings**: 70-82% | **Setup**: 1 day | **Cost**: $0-500

### Use Case: Production RAG System
**Recommendation**: Provence + Semantic Caching + Model Routing  
**Savings**: 60-75% | **Setup**: 2-3 days | **Cost**: $2-5k/year

---

## 📚 Guides

- **[Getting Started](docs/GETTING_STARTED.md)** — Choose your first tool
- **[Benchmark Methodology](docs/BENCHMARKS.md)** — How we measure savings
- **[Integration Patterns](docs/INTEGRATION_PATTERNS.md)** — Layering tools together
- **[Vendor Comparison](docs/VENDOR_COMPARISON.md)** — Licensed vs Open-Source
- **[Cost Calculator](docs/COST_CALCULATOR.md)** — Estimate savings for your use case

---

## 🔄 Updates

**Last updated**: 2026-08-11  
**Tools tracked**: 20+  
**Coverage**: Production-only (no research-stage tools)

**What's new in 2026**:
- ✅ Prompt caching matured (Anthropic native, 90% cached)
- ✅ Semantic caching production-ready (Bifrost, 20-45% hits)
- ✅ Model routing sophisticated (RouteLLM, 85% savings)
- ✅ KV cache pruning validated (SlimInfer, AAAI 2026)

---

## 💬 Contributing

See [CONTRIBUTING.md](CONTRIBUTING.md) for:
- Adding new tools
- Submitting benchmarks
- Reporting inaccuracies

---

## 📄 License

MIT — Open for research, learning, and production use.

---

## 🙏 Acknowledgments

Research compiled from:
- Published benchmarks (AAAI 2026, NeurIPS 2025)
- Production deployments (37% of enterprises use 5+ models)
- Open-source communities (LLMLingua, vLLM, LiteLLM)
- Vendor documentation (Anthropic, OpenAI, Together AI)

**Disclaimer**: This tracker reflects 2026 state of art. Comparisons are snapshot-based; tools evolve rapidly. Verify benchmarks for your specific use case before production deployment.
