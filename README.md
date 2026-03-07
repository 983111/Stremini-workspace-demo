# Stremini Workspace

Stremini Workspace is a comprehensive, AI‑native ecosystem designed to empower startups, developers, and researchers. It provides a suite of specialized autonomous agents that handle everything from system architecture and code generation to competitive intelligence and legal compliance.

## 🚀 Project Overview

The project is structured as a unified workspace (`index.html`) that serves as a portal to various high‑intelligence agents. Each agent is a specialized tool optimized for a specific domain of business or technical operations.

## The Four Layers of Intelligence

The workspace is organized into four strategic layers:

- **Intelligence Layer:** Deep research, data analysis, and competitive monitoring.
- **Product Layer:** Architecture design, product building, and workflow automation.
- **Growth Layer:** Market intelligence, GTM strategy, and financial modeling.
- **Operational Layer:** Legal compliance and personal OS management.

## 🤖 Specialized Agents

### 1. Technical & Engineering Agents
- **Architect Agent** (`Architect.html`): Designs high‑level system architectures and provides implementation roadmaps.
- **Code Agent** (`Code-agent.html`): Performs code implementation, debugging, security reviews, and logic explanations.
- **Product Builder** (`product.html`): Generates PRDs, database schemas, frontend components, and deployment strategies.
- **AI Model Evaluator** (`model-evaluator.html`): Benchmarks AI models, detects hallucinations, and compares model performance.

### 2. Business & Strategy Agents
- **Competitive Intel** (`compeititve.html`): Monitors competitors in real‑time, analyzes market threats, and identifies opportunities.
- **Growth Intelligence** (`Growth.html`): Builds GTM plans, viral loops, and ad strategies while monitoring funnel conversion.
- **Financial Agent** (`FinAgent.html`): Conducts financial modeling, burn‑rate analysis, and runway forecasting.
- **Startup Legal & Strategy** (`Startup-Legal-Compliance-Agent.html`): Drafts contracts, privacy policies, and ensures regulatory compliance.

### 3. Data & Research Agents
- **Data Intelligence** (`Data.html`): Performs cohort analysis, anomaly detection, and automated forecasting from CSV data.
- **Research & Math** (`Research.html`): Solves complex mathematical proofs and conducts academic‑grade technical research.
- **Knowledge Graph** (`knowledge.html`): Maps semantic connections between data points to synthesize new insights.

### 4. Automation & Productivity
- **Automation Builder** (`automation.html`): An AI‑native workflow builder for creating autonomous business processes.
- **Personal OS** (`Personal-os.html`): Manages habits, goals, and long‑term memory for founders (codenamed ARIA).

## 🛠 Technical Stack

- **Frontend:** Modern HTML5, CSS3 (using custom variables for theming), and vanilla JavaScript.
- **Typography:** Professional serif (Lora) and sans‑serif (DM Sans) pairings for high readability.
- **Libraries:**
  - **Highlight.js:** Syntax highlighting for code outputs.
  - **Mermaid.js:** Rendering architectural diagrams.
  - **PDF.js & Mammoth:** Parsing uploaded documents and research papers.
- **Backend:** Powered by Cloudflare Workers (e.g., `*.vishwajeetadkine705.workers.dev` endpoints).

## 🎨 UI/UX Features

- **Mode‑Specific Interfaces:** Each agent features a tailored UI with distinct color themes (e.g., Violet for Knowledge, Amber for Architect, Indigo for Automation).
- **Report System:** Agents generate structured, interactive reports with “Health Scores” and critical flags.
- **Interactive Workspaces:** Real‑time “Thinking” states and action cards provide feedback during complex AI tasks.
- **Multi‑Modal Exports:** Support for downloading insights as JSON, PDF, or copying to clipboard.

## 📂 Project Structure

```plaintext
Plaintext
├── index.html           # Main Workspace Portal
├── Architect.html       # System Design Agent
├── Code-agent.html      # Programming Assistant
├── Data.html            # Data Analysis Engine
├── Research.html        # Academic/Math Researcher
├── FinAgent.html        # Financial Modeler
├── Growth.html          # Marketing & GTM Agent
├── automation.html      # Workflow Builder
├── compeititve.html     # Market Monitoring
├── knowledge.html       # Knowledge Synthesis
├── model-evaluator.html # AI Benchmarking Tool
├── Personal-os.html     # Founder Productivity Tool
├── product.html         # PRD & Prototyping Agent
└── Startup-Legal-Compliance-Agent.html # Legal Agent
```

## 🚦 Getting Started

- **Deployment:** The workspace is built as a static frontend that interacts with Cloudflare Worker backends. Simply host the HTML files on any static hosting provider.
- **API Configuration:** Update the `BACKEND` constants in the `<script>` sections of the HTML files to point to your specific AI service endpoints.
- **Usage:** Open `index.html` to navigate the layers and launch the specific agent needed for your task.
