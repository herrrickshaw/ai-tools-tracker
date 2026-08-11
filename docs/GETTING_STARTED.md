# Getting Started with AI Token Optimization

**Goal**: Pick the right tool(s) for your use case in 5 minutes.

---

## Quick Self-Assessment

Answer these 3 questions:

### 1. What's your primary constraint?
- **Token count** → Compression tool (LLMLingua-2)
- **Cost** → Model routing (RouteLLM)
- **Latency** → Native caching (Prompt Caching)
- **Complexity** → Budget tracker (Token Optimizer)

### 2. How many LLM vendors do you use?
- **Only Claude** → Use Prompt Caching + Budget Tracker
- **2-3 vendors** → Use routing + semantic caching
- **5+ vendors** → Use full AI gateway (Portkey, LiteLLM)

### 3. What's your deployment model?
- **Personal/Solo** → Local-first tool (Token Optimizer)
- **Startup/Small team** → Open-source stack
- **Enterprise** → Managed gateway (Portkey, Langfuse)

---

## Recommended Stacks

### Stack 1: Solo Dev (Best Starting Point)

```
Anthropic Prompt Caching
    ↓
Budget Tracker (Token Optimizer)
    ↓
Optional: Semantic Caching
```

**Savings**: 60-75% | **Setup**: 2 hours | **Cost**: $0

**Install**:
```bash
# Token Optimizer budget tracker
python3 ~/.claude/scripts/token_budget.py --reset

# Optional: Add semantic caching
pip install sentence-transformers
```

**Expected**: Session starts with budget initialized, queries cached, savings tracked.

---

### Stack 2: Cost-Conscious Dev

```
Token Optimizer (Markitdown conversion)
    ↓
RouteLLM (Model routing)
    ↓
Semantic Caching (Query dedup)
```

**Savings**: 70-82% | **Setup**: 1 day | **Cost**: $500-2k

**Install**:
```bash
# Token Optimizer setup
python3 ~/.claude/scripts/integrate_graph_and_dropbox.py --setup-dropbox

# Add RouteLLM
pip install routellm

# Add semantic caching
pip install bifrost-cache
```

---

### Stack 3: Multi-Repo Research

```
Token Optimizer (Full system)
    ↓
LLMLingua-2 (Compression layer)
    ↓
Semantic Caching (Query cache)
    ↓
Langfuse (Observability)
```

**Savings**: 75-85% | **Setup**: 2-3 days | **Cost**: $0-500/year

**Install**:
```bash
# Full Token Optimizer
pip install markitdown llmlingua2 sentence-transformers

# Observability
pip install langfuse
```

---

### Stack 4: Enterprise/SaaS

```
Portkey or LiteLLM (AI Gateway)
    ├─ RouteLLM (Model routing)
    ├─ Semantic Caching (Bifrost/Redis)
    └─ Prompt Caching (native)
         ↓
Langfuse (Budget + monitoring)
```

**Savings**: 70-85% | **Setup**: 1-2 days | **Cost**: $5-15k/year

---

## Step-by-Step: Start with Stack 1 (Solo Dev)

### Step 1: Verify You're Using Claude (5 min)

```python
import anthropic

client = anthropic.Anthropic()
print(client.models.retrieve("claude-3-5-sonnet-20241022"))
# If this works, you're ready
```

### Step 2: Enable Prompt Caching (5 min)

```python
# Native Anthropic caching (built-in to SDK >= 0.28)
message = client.messages.create(
    model="claude-3-5-sonnet-20241022",
    max_tokens=1024,
    system=[
        {
            "type": "text",
            "text": "You are a helpful assistant.",
            "cache_control": {"type": "ephemeral"}  # Enable caching
        }
    ],
    messages=[
        {
            "role": "user",
            "content": "Explain token optimization"
        }
    ]
)
print(f"Cache creation tokens: {message.usage.cache_creation_input_tokens}")
print(f"Cache read tokens: {message.usage.cache_read_input_tokens}")
```

**Expected**: First request uses cache_creation_input_tokens (higher cost). Subsequent identical requests use cache_read_input_tokens (90% cheaper).

### Step 3: Add Budget Tracking (10 min)

```bash
# Initialize Token Optimizer budget tracker
python3 ~/.claude/scripts/token_budget.py --reset

# See stats
python3 ~/.claude/scripts/token_budget.py --stats
```

**Expected output**:
```
═══════════════════════════════════════════════════════════
                TOKEN OPTIMIZATION STATUS
═══════════════════════════════════════════════════════════
Budget initialized:         200,000 tokens
Estimated turns left:       45 turns @ 4,500 avg tokens/turn
Prompt caching savings:     37% this session
═══════════════════════════════════════════════════════════
```

### Step 4: Optional: Add File Conversion (15 min)

```bash
# If you read PDFs, DOCX, JSON in your sessions:
python3 ~/.claude/scripts/convert_files.py ~/reports/*.pdf -o ./md

# See how much space you saved
python3 ~/.claude/scripts/integrate_graph_and_dropbox.py --stats
```

---

## Validating Your Setup

### Test 1: Caching is Working

```python
# Same system prompt + message = should use cache

response1 = client.messages.create(
    model="claude-3-5-sonnet-20241022",
    max_tokens=100,
    system=[{"type": "text", "text": "You are helpful.", "cache_control": {"type": "ephemeral"}}],
    messages=[{"role": "user", "content": "Hello"}]
)

response2 = client.messages.create(
    model="claude-3-5-sonnet-20241022",
    max_tokens=100,
    system=[{"type": "text", "text": "You are helpful.", "cache_control": {"type": "ephemeral"}}],
    messages=[{"role": "user", "content": "Hello"}]
)

print(f"Request 1: {response1.usage.cache_creation_input_tokens} creation tokens")
print(f"Request 2: {response2.usage.cache_read_input_tokens} read tokens (should be >0)")
```

**Expected**: Request 2 has `cache_read_input_tokens > 0`

### Test 2: Budget Tracking is Working

```bash
# Run a quick test session
python3 -c "
from anthropic import Anthropic
client = Anthropic()
for i in range(3):
    response = client.messages.create(
        model='claude-3-5-sonnet-20241022',
        max_tokens=50,
        messages=[{'role': 'user', 'content': 'Count to 5'}]
    )
    print(f'Request {i+1}: {response.usage.input_tokens + response.usage.output_tokens} tokens')
"

# Check budget
python3 ~/.claude/scripts/token_budget.py --stats
```

**Expected**: Budget decreases after each request

---

## Common Issues

### Issue: "Cache not working"
- **Check**: Are you using `cache_control` in system messages?
- **Fix**: Add `"cache_control": {"type": "ephemeral"}` to system text
- **Note**: Caching requires 1,024+ token prefix minimum

### Issue: "Budget tracker not showing savings"
- **Check**: Are you actually using Prompt Caching?
- **Fix**: Follow Step 2 above (enable `cache_control`)
- **Note**: Only cached requests show savings

### Issue: "File conversion is slow"
- **Check**: File size (PDFs >10MB are slow)
- **Fix**: Use `--limit 5` to test with 5 small files first
- **Note**: Async conversion available in Token Optimizer v2

---

## Next Steps (Week 2+)

Once you confirm Step 1-4 work:

1. **Monitor for a week** — See actual savings in your sessions
2. **Experiment with Stack 2** — Add RouteLLM for multi-vendor cost arbitrage
3. **Run benchmarks** — Validate claims on your documents
4. **Share results** — Blog/write about your optimization journey

---

## Resources

- [Anthropic Prompt Caching Docs](https://docs.anthropic.com/en/docs/build-a-chatbot-with-multi-turn-conversation#caching)
- [Token Optimizer Repository](https://github.com/herrrickshaw/global-market-research-platform/tree/token-optimizer)
- [Full Competitive Analysis](COMPETITIVE_ANALYSIS.md)

---

**Estimated time to 60% savings**: 1 day  
**Estimated time to 80% savings**: 1 week  
**Estimated time to 90% savings**: 1 month (requires multi-vendor setup)
