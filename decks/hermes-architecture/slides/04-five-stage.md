# 🔗 Five-Stage Analysis Chain

> N items × 5 calls · Context → 4-Agent (Positive / Negative / Risk / Trade-off) → **Conclusion**

---

## The Five Stages

<div class="flow-tree">
<span class="node">[Stage 1: Context]</span>
    Inputs (data, scores, metrics)
       │  parse environment, surface assumptions
       ▼
    Context summary

<span class="node">[Stages 2-5: parallel agents]</span>

    Context
       ├──► Positive  (bull case)
       ├──► Negative  (bear case)
       ├──► Risk      (downside scenarios)
       └──► Trade-off (competing objectives)

       ▼
    Conclusion
       (action + confidence + alternatives + rationale)
</div>

<div class="small">

Each stage is an **independent LLM call**. Outputs flow forward into the final conclusion.

</div>

---

## Conclusion Output

| Input | Output |
|---|---|
| Positive / Negative summary | recommended action |
| Risk scenarios | confidence (%) |
| Trade-off matrix | alternative options |
| Metrics / scores | rationale |

---

## Cost Optimization

| Item | Value |
|---|---:|
| **Per run** | **$0.054** |
| Calls per analysis | 5 – 6 |
| Daily calls (N items) | N × 6 |
| Monthly (22 business days) | $1.20 |
| **Share of monthly budget** | **4%** |

<div class="small">

💡 **V4 Flash** (DeepSeek) at temperature 0.3 = consistency at 95% lower cost

</div>