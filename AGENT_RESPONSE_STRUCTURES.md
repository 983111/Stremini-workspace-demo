# StreminiAI — Agent Response Structure Documentation

This file documents how each backend is expected to respond, based on how the current frontend files parse and render responses.

---

## 1) Shared transport contract

Across agents, requests are sent as `POST` JSON and almost all handlers inspect a top-level `status` field.

Common envelope pattern:

```json
{
  "status": "...",
  "content": "...",
  "message": "...",
  "solution": "...",
  "data": { }
}
```

- `status` drives renderer branch selection.
- `ERROR` is the canonical failure branch for most agents, using `message`.
- Most text-first agents render `content` (fallbacks: `solution`, `reply`, `message`).

---

## 2) Agent-by-agent response contracts (15 agents in unified chatbot)

## 2.1 Research Agent
- **Endpoint:** `https://agentic-research.vishwajeetadkine705.workers.dev`
- **Modes:** `research`, `math`
- **Request shape:** `{ query, mode, history, iteration }`
- **Expected statuses:**
  - `PAPER` → structured long-form paper in `content`.
  - `SOLUTION` → math solution in `content`.
  - `COMPLETED` → plain text fallback in `solution`.
  - `ERROR` → error payload in `message`.
- **Renderer expectations:**
  - `PAPER` / `SOLUTION`: parse markdown-like sections/diagrams from `content`.
  - `COMPLETED`: render plain paragraph.

## 2.2 Data Agent
- **Endpoint:** `https://data-agent.vishwajeetadkine705.workers.dev`
- **Modes:** `diagnose`, `cohort`, `conversion`, `anomaly`, `forecast`, `csv`
- **Request shape:** `{ query, mode, history, iteration }`
- **Expected statuses:**
  - `REPORT` with `data` object.
  - `RAW` with unparsed text in `content`.
  - `COMPLETED` with `solution`.
  - `ERROR` with `message`.
- **`REPORT.data` fields consumed by UI:**
  - `title`, `summary`, `health_score`, `health_label`, `sections[]`.
  - per-section renderer supports arrays such as: `insights`, `flags`, `benchmarks`, `experiments`, `scenarios`, `anomalies`, `causes`, `funnel_steps`, `milestones`, `items`.

## 2.3 Knowledge Agent
- **Endpoint:** `https://knowledge.vishwajeetadkine705.workers.dev`
- **Modes:** `add`, `connect`, `explore`, `gaps`, `synthesize`, `teach`
- **Request shape:** `{ query, mode, history, userKnowledge, response_format: "structured_json" }`
- **Expected statuses:**
  - Graph-like statuses mapped by frontend: `NODE_ADDED`, `CONNECTIONS`, `EXPLORATION`, `GAPS_FOUND`, `SYNTHESIS`, `USER_KNOWLEDGE`.
  - `ERROR`.
- **Graph payload fields consumed:**
  - `graph.nodes[]`, `graph.edges[]`, `graph.insights[]`.
  - Optional top-level rich fields: `summary`, `nodes`, `edges`, `insights`, `suggestions`, `prose`.
- **Node fields used:** `title|name`, `description`, `type`, `weight`, `domain`.
- **Edge fields used:** `from`, `to`, `relation`, `strength`.

## 2.4 Dataset Builder
- **Endpoint:** `https://stremini-dataset.vishwajeetadkine705.workers.dev`
- **Modes:** `full`, `collect`, `clean`, `label`, `quality`, `augment`, `export`
- **Request pattern:**
  - Initialize: `{ action:"initialize", goal, mode }`
  - Chat: `{ action:"chat", message, history, mode }`
- **Expected statuses:**
  - `INITIALIZED` for startup handshake.
  - `REPLY` for ongoing interaction.
- **Payload fields consumed:**
  - `reply` (rich markdown-like content), `history`, `summary`, `pipeline`.

## 2.5 Competitive Intelligence
- **Endpoint:** `https://compeititve.vishwajeetadkine705.workers.dev`
- **Modes:** `monitor`, `report`, `threats`, `opportunities`, `hiring`, `deep`
- **Request shape:** `{ query, mode, history, iteration }`
- **Expected statuses:**
  - `ERROR`.
  - success branch using either `report` object or `content`.
- **Structured report fields consumed:**
  - `executive_summary`
  - `scores[]` (`label`, `value`, `trend`, `change`)
  - `company_profiles[]` (`name`, `tagline|sector`, `funding`, `employees`, `founded`, `hq`, `summary`, `type`)
  - `signals[]`, `threats[]`, `opportunities[]`, `hiring_trends[]`, `tech_shifts[]`, `recommendations[]`, `sources[]`.

## 2.6 Concept Explainer
- **Endpoint:** `https://stremini-concept.vishwajeetadkine705.workers.dev`
- **Modes:** visual type driven (`auto|flow|map|timeline|compare`) via `vizType`
- **Request shape:** `{ concept, vizType, history }`
- **Expected statuses:**
  - `OK`
  - non-OK branch uses `message` as error.
- **Success payload fields consumed:**
  - `title`, `subtitle`, `vizType`, `visualization`, `explanation`, `keyConcepts[]`, `analogy`.

## 2.7 AI Architect
- **Endpoint:** `https://ai-architect.vishwajeetadkine705.workers.dev`
- **Modes:** `architecture`, `rag`, `agent`, `cost`, `diagnose`, `anomaly`, `forecast`, `csv`
- **Request shape:** `{ query, mode, history, iteration }`
- **Expected statuses:**
  - `REPORT` with `data` object.
  - `BLUEPRINT` or `SOLUTION` as text-first outputs.
  - `RAW` with `content`.
  - `COMPLETED` with `solution`.
  - `ERROR` with `message`.
- **`REPORT.data` fields consumed:**
  - `type`, `title`, `summary`, `health_score`, `health_label`, `sections[]`.
  - section entries render `label`, `icon`, `content`, plus rich arrays like `insights`.

## 2.8 Code Agent
- **Endpoint:** `https://k2-code-agent.vishwajeetadkine705.workers.dev`
- **Modes:** `implement`, `review`, `debug`, `explain`
- **Request shape:** `{ query, mode, history }` (mode-specific prompting in UI)
- **Expected statuses:**
  - `CODE` → implement renderer
  - `REVIEW` → review renderer
  - `DEBUG` → debug renderer
  - `EXPLANATION` → explanation renderer
  - `COMPLETED` with `solution`
  - `ERROR` with `message`
- **Success payload field:** primarily `content`.

## 2.9 Product Builder
- **Endpoint:** `https://product-builder.vishwajeetadkine705.workers.dev`
- **Modes:** `full`, `prd`, `schema`, `frontend`, `deployment`
- **Request shape:** `{ idea, phase, history }`
- **Expected statuses:**
  - `PRODUCT_BUILT` with `data` object
  - `COMPLETED` with `solution`
  - `ERROR` with `message`
- **`PRODUCT_BUILT.data` is rendered as multi-section product output (PRD/schema/frontend/deploy depending on phase).**

## 2.10 Automation Builder
- **Endpoint:** `https://automation-builder.vishwajeetadkine705.workers.dev`
- **Modes:** `build`, `explain`, `debug`, `optimize`, `chain`, `integrate`
- **Request shape:**
  `{ query, mode, history, automationContext:{ complexity, runtime, trigger, goal, services } }`
- **Expected statuses:**
  - Any non-`ERROR` status is treated as success in current frontend.
  - `ERROR` with `message`.
- **Success payload field consumed:**
  - `content` (fallback `solution`) as long-form text/markdown/code.
- **Renderer behavior:**
  - Parses code fences.
  - For `build` / `chain`, extracts workflow steps (`STEP n`, `AGENT n`, trigger lines) to visualize flow.

## 2.11 Model Evaluator
- **Endpoint:** `https://model-evaluator.vishwajeetadkine705.workers.dev`
- **Modes:** `evaluate`, `compare`, `hallucination`, `benchmark`, `score`
- **Request shape:** `{ mode, prompt, responseA, responseB, modelA, modelB }`
- **Expected statuses:**
  - Structured: `EVALUATION`, `COMPARISON`, `HALLUCINATION`, `BENCHMARK`, `SCORE`, `COMPLETED`
  - `ERROR`
- **Success payload field consumed:** `content` (sectioned markdown-like text).

## 2.12 Startup & Legal Agent (combined in unified chatbot)
- **Strategy endpoint:** `https://startup-strategy.vishwajeetadkine705.workers.dev`
- **Legal endpoint:** `https://legal-compliance.vishwajeetadkine705.workers.dev`
- **Modes:**
  - Strategy: `business_model`, `revenue`, `market`, `pitch`, `swot`
  - Legal: `contract`, `tnc`, `privacy`, `compliance`
- **Request shape (strategy):** `{ mode, query, context:{industry,stage,location,targetMarket}, responseFormat:"structured_actionable" }`
- **Request shape (legal):** `{ mode, query, documentText, jurisdiction, entityType, responseFormat:"structured_actionable" }`
- **Expected statuses:**
  - Structured: `BUSINESS_MODEL`, `REVENUE`, `MARKET`, `PITCH`, `SWOT`, `CONTRACT`, `TNC`, `PRIVACY`, `COMPLIANCE`, `COMPLETED`
  - `ERROR`
- **Success payload field consumed:** `content`.

## 2.13 Growth Agent
- **Endpoint:** `https://growth-agent.vishwajeetadkine705.workers.dev`
- **Modes:** `gtm`, `competitor`, `viral`, `ads`, `funnel`
- **Request shape:** `{ query, mode, history, iteration }`
- **Expected statuses:**
  - `REPORT` with `data`
  - `RAW` with `content`
  - `COMPLETED` with `solution`
  - `ERROR` with `message`
- **`REPORT.data` fields consumed:**
  - `title`, `sections[]` and section-rich arrays (e.g., `competitors`, `loops`, `creatives`, `stages`, `items`) depending on mode.

## 2.14 Finance Agent
- **Endpoint:** `https://agentic-finance.vishwajeetadkine705.workers.dev`
- **Modes:** `budget`, `generic`
- **Request pattern:**
  - Initialize with CSV: `{ action:"initialize", mode, csvData, filename }`
  - Chat: `{ action:"chat", message, history, responseFormat:"structured_actionable" }`
- **Expected statuses:**
  - `INITIALIZED` for CSV bootstrap.
  - `REPLY` for conversational output.
- **Payload fields consumed:**
  - Init: `rowsLoaded`, `filename`, optional `summary` (with `mode` and `insights[]`).
  - Chat: `reply`, `history`.
- **Formatting expectation:** reply should follow sectioned actionable format (summary, key numbers, recommendations, risks, next 7 days).

## 2.15 Personal OS
- **Endpoint:** `https://personal-os.vishwajeetadkine705.workers.dev`
- **Modes:** `chat`, `goals`, `habits`, `reflect`, `plan`, `memory` (mapped in UI)
- **Request shape:**
  `{ query, mode, history, memory, context:{ currentGoals, recentHabits, pendingDecisions } }`
- **Expected statuses:**
  - Structured: `GOALS`, `HABITS`, `REFLECT`, `PLAN`, `MEMORY`, `CHAT`, `COMPLETED`
  - `ERROR`
- **Success payload field consumed:** `content` (fallback `solution`).
- **Frontend behavior:** parsed into sections and optionally mined into local memory buckets (`goals`, `habits`, `decisions`, `insights`).

---

## 3) Unified chatbot (`chatbot.html`) compatibility notes

The unified chatbot currently routes by selected agent and mode and then normalizes output to:

1. `data.content`
2. fallback `data.reply`
3. fallback `data.message`
4. fallback `JSON.stringify(data)`

For maximum compatibility across all 15 backends:

- Always include `status`.
- Prefer placing primary human-readable output in `content`.
- For report agents, include structured `data` object with stable key names noted above.
- Keep `ERROR` responses in shape `{ status:"ERROR", message:"..." }`.

