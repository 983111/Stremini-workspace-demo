# StreminiAI Backend Endpoints (15 Agents)

This document lists the backend worker endpoints used by the **15-agent unified chatbot**.

## Agent endpoint matrix (used by `chatbot.html`)

| # | Agent | Frontend file(s) | Worker endpoint(s) |
|---|---|---|---|
| 1 | Research Agent | `Research.html` | `https://agentic-research.vishwajeetadkine705.workers.dev` |
| 2 | Data Agent | `Data.html` | `https://data-agent.vishwajeetadkine705.workers.dev` |
| 3 | Knowledge Agent | `knowledge.html` | `https://knowledge.vishwajeetadkine705.workers.dev` |
| 4 | Dataset Builder | `dataset-builder.html` | `https://stremini-dataset.vishwajeetadkine705.workers.dev` |
| 5 | Competitive Intelligence | `compeititve.html` | `https://compeititve.vishwajeetadkine705.workers.dev` |
| 6 | Concept Explainer | `conept.html` | `https://stremini-concept.vishwajeetadkine705.workers.dev` |
| 7 | AI Architect | `Architect.html` | `https://ai-architect.vishwajeetadkine705.workers.dev` |
| 8 | Code Agent | `Code-agent.html` | `https://k2-code-agent.vishwajeetadkine705.workers.dev` |
| 9 | Product Builder | `product.html` | `https://product-builder.vishwajeetadkine705.workers.dev` |
| 10 | Automation Builder | `automation.html` | `https://automation-builder.vishwajeetadkine705.workers.dev` |
| 11 | Model Evaluator | `model-evaluator.html` | `https://model-evaluator.vishwajeetadkine705.workers.dev` |
| 12 | Startup & Legal Agent | `Startup-Legal-Compliance-Agent.html` | Strategy: `https://startup-strategy.vishwajeetadkine705.workers.dev`<br/>Legal: `https://legal-compliance.vishwajeetadkine705.workers.dev` |
| 13 | Growth Agent | `Growth.html` | `https://growth-agent.vishwajeetadkine705.workers.dev` |
| 14 | Finance Agent | `FinAgent.html` | `https://agentic-finance.vishwajeetadkine705.workers.dev` |
| 15 | Personal OS | `Personal-os.html` | `https://personal-os.vishwajeetadkine705.workers.dev` |

## Routing behavior for Startup & Legal

In the unified `chatbot.html` implementation:

- Strategy modes (`business_model`, `revenue`, `market`, `pitch`, `swot`) route to `startup-strategy...workers.dev`.
- Legal modes (`contract`, `tnc`, `privacy`, `compliance`) route to `legal-compliance...workers.dev`.

