# AI Strategic Insight Discovery System

> **Using Frontier AI to Derive Non-Obvious Strategic Implications from Scientific and Technical Knowledge**
> 
> Built as part of the MATS Application — Jeff Alstott Research Stream

---

## What This Is

A multi-stage AI pipeline that reads scientific literature and surfaces **non-obvious strategic implications** — cross-domain insights connecting scientific advances to geopolitics, labour markets, national security, and economic power — before those implications become obvious to human analysts.

The system does not summarise papers. It reasons across them.

---

## How It Works

```
arXiv Papers
     │
     ▼
┌─────────────────┐    ┌──────────────────────┐
│  Vector Store   │    │   Knowledge Graph    │
│  (ChromaDB)     │    │   (NetworkX)         │
└────────┬────────┘    └──────────┬───────────┘
         │                        │
         └──────────┬─────────────┘
                    │  Cross-domain context
                    ▼
           ┌─────────────────┐
           │   Hypothesis    │  LLaMA 3.3-70B via Groq
           │   Generator     │
           └────────┬────────┘
                    │
                    ▼
           ┌─────────────────┐
           │  Multi-Agent    │  Proposer vs Skeptic vs Expert
           │  Debate (×2)    │
           └────────┬────────┘
                    │
                    ▼
           ┌─────────────────┐
           │  Falsification  │  Counter-evidence retrieval
           │  Engine         │
           └────────┬────────┘
                    │  Filter confidence < 0.35
                    ▼
           ┌─────────────────┐
           │   Strategic     │  Policy · Economic · Security
           │   Abstraction   │  + 2nd-order effects + timeline
           └────────┬────────┘
                    │
                    ▼
           Strategic Insight Report
```

**Three core techniques combined:**

1. **Multi-Agent Debate** (Du et al., 2023) — Proposer, Skeptic, and Domain Expert agents with asymmetric context, forcing genuine adversarial pressure on each hypothesis
2. **RAG + Knowledge Graph Traversal** (Lewis et al., 2020) — Semantic retrieval augmented with explicit cross-domain bridge node discovery
3. **Falsification-Driven Hypothesis Testing** — Active counter-evidence retrieval to stress-test each hypothesis before elevation to strategic insight

---

## Repository Structure

```
AI-Strategic-Insight/
│
├── AI Strategic Insight.ipynb          # Full pipeline — all stages, outputs included
│
├── outputs/
│   ├── strategic_insights.json         # Raw pipeline output (5 insights)
│   ├── strategic_insights_evaluated.json  # Insights with LLM-as-judge scores
│   └── backtest_results.json           # Historical backtesting results
│
└── images/
    ├── Full Knowledge Graph.png        # 167-node knowledge graph visualisation
    ├── Confidence Score.png            # Post-falsification confidence bar chart
    └── EVALUATION FRAMEWORK.png        # Insight quality radar chart (5 dimensions)
```

---

## Results

Applied to **protein folding and synthetic biology** (30 arXiv papers):

| # | Domain Connection | Confidence | Time Horizon |
|---|-------------------|-----------|--------------|
| 1 | Biological sciences → Geopolitics of supply chains | 40% | 10–20 years |
| 2 | Computer science → Labour markets | 70% | 10–20 years |
| 3 | Biological sciences → Public health & economic power | 55% | 10–20 years |
| 4 | Synthetic biology → National security | 60% | 10–20 years |
| 5 | Environmental policy → Technological competition | 70% | 20+ years |

**Knowledge graph:** 167 nodes, 158 edges extracted from 30 papers

**Historical backtesting:** 50% anticipation score on CRISPR biosecurity implications from 2014 pre-cutoff literature

**Evaluation:** LLM-as-judge scores confirm pipeline outputs higher than naive one-shot prompting on novelty and cross-domain depth

---

### Knowledge Graph
![Knowledge Graph](images/Full%20Knowledge%20Graph.png)

### Confidence Scores
![Confidence Scores](images/Confidence%20Score.png)

### Evaluation Radar Chart
![Evaluation Framework](images/EVALUATION%20FRAMEWORK.png)

---

## Quickstart

### 1. Get a Free Groq API Key
Sign up at [console.groq.com](https://console.groq.com) — free, no credit card required.

### 2. Open in Google Colab
[![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/JitUikey28/AI-Strategic-Insight/blob/main/AI%20Strategic%20Insight.ipynb)

### 3. Add Your API Key
In Colab, click the 🔑 key icon in the left sidebar → Add new secret:
- Name: `GROQ_API_KEY`
- Value: your key from console.groq.com
- Toggle "Notebook access" ON

### 4. Run All Cells
Run cells in order, top to bottom. The pipeline takes approximately **20–30 minutes** on free Colab for the full run (5 hypotheses × 2 debate rounds).

### 5. Change the Topic
Edit the `TOPIC` and `ARXIV_QUERIES` variables in the configuration cell to analyse any scientific domain:

```python
TOPIC = "advances in protein folding and synthetic biology"

ARXIV_QUERIES = [
    "protein folding deep learning AlphaFold",
    "synthetic biology biomanufacturing",
    "CRISPR gene editing applications",
]
```

---

## Configuration

Key parameters in `CONFIG` (adjust for speed vs. quality):

| Parameter | Default | Notes |
|-----------|---------|-------|
| `model` | `llama-3.3-70b-versatile` | Groq free tier |
| `num_papers` | `10` | Papers per query — keep ≤ 15 on free Colab |
| `num_hypotheses` | `5` | Hypotheses to generate |
| `debate_rounds` | `2` | Rounds per hypothesis — reduce to 1 for speed |
| `falsification_threshold` | `0.35` | Reject below this confidence |
| `sleep_between_calls` | `1.5` | Seconds — respects Groq free tier rate limits |

**Speed tip:** Set `num_hypotheses = 3` and `debate_rounds = 1` for a ~10-minute run.

---

## Notebook Structure

| Stage | Description |
|-------|-------------|
| Stage 0 | Setup & Installation |
| Stage 1 | LLM Wrapper (Groq API + retry logic) |
| Stage 2 | Data Ingestion (arXiv API) |
| Stage 3 | Vector Database (ChromaDB) |
| Stage 4 | Knowledge Graph (NetworkX) |
| Stage 5 | Hypothesis Generation |
| Stage 6 | Multi-Agent Debate (Proposer / Skeptic / Expert / Judge) |
| Stage 7 | Falsification Loop |
| Stage 8 | Strategic Abstraction |
| Stage 9 | Full Pipeline Orchestrator |
| Stage 10 | Display & Evaluation Utilities |
| Bonus | Evaluation Framework (LLM-as-judge, radar chart) |
| Bonus | Historical Backtesting |
| Bonus | Baseline Comparison |

---

## Tech Stack

| Component | Tool |
|-----------|------|
| LLM | LLaMA 3.3-70B via [Groq](https://groq.com) (free) |
| Embeddings | all-MiniLM-L6-v2 (sentence-transformers) |
| Vector Store | ChromaDB (in-memory) |
| Knowledge Graph | NetworkX (in-memory) |
| Data Source | arXiv API (free, no key required) |
| Environment | Google Colab free tier |
| Language | Python 3.10+ |

No GPU required. No paid APIs. No external databases.

---

## Limitations

- **LLM-as-judge circularity:** The evaluator and generator use the same model family. Human expert validation is the most important next step.
- **arXiv coverage bias:** arXiv over-represents physics, math, and CS. Fields like policy and social science are underrepresented, which limits some backtesting cases.
- **Corpus size:** 30 papers is a proof of concept. A production system would need 500–1000+ papers per topic for meaningful graph density.
- **Causal shallowness:** Hypotheses are structurally cross-domain but sometimes causally under-specified. This is the identified weakest link — see proposal for detail.

---

## Proposal Document

Full research proposal with complete methodology, all 5 strategic insights, evaluation scores, backtesting analysis, and future research agenda:

[View Proposal Document](https://docs.google.com/document/d/1-b36vIfYb2wdz-KNLIKRcJEBgRSHtzX-/edit?usp=drive_link&ouid=106361518792433288565&rtpof=true&sd=true)

---

## License

MIT License — free to use, modify, and build on.

---

*Built for the MATS Program — Jeff Alstott Research Stream*
