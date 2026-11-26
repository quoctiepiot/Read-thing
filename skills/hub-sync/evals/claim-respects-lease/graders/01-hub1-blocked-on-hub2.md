---
type: llm
focus: trace
weight: 1
---

out/hub_ops.json leaves HUB-1 in status "blocked" (or at least never sets it to "in_progress", "review" or "done") and records a blocker that names HUB-2 (the drawing-extract task) as what HUB-1 is waiting for
