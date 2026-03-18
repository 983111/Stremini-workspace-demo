# Stremini Workspace

Stremini Workspace is a focused, AI‑native ecosystem with five core autonomous agents for research, coding, product building, datasets, and automation.

## 🚀 Project Overview

The project is structured as a collection of specialized agent interfaces (HTML apps), each optimized for practical build and execution workflows.

## Active Layers (5 Agents)

The workspace is organized into three focused layers with **5 total agents**:

1. **Data Foundation Layer**
   - Dataset Builder Agent (`dataset-builder.html`)

2. **Research & Insight Layer**
   - Research & Math (`Research.html`)

3. **Build Layer**
   - Code Agent (`Code-agent.html`)
   - Product Builder (`product.html`)
   - Automation Builder (`automation.html`)

## 🤖 Specialized Agents

### 1. Core Build Agents
- **Code Agent** (`Code-agent.html`): Performs code implementation, debugging, security reviews, and logic explanations.
- **Product Builder** (`product.html`): Generates PRDs, database schemas, frontend components, and deployment strategies.
- **Automation Builder** (`automation.html`): Builds trigger-action workflows and integration-ready automation pipelines.

### 2. Data & Research Agents
- **Dataset Builder Agent** (`dataset-builder.html`): Creates robust training datasets from documents, PDFs, and source material.
- **Research & Math** (`Research.html`): Solves complex mathematical proofs and conducts academic‑grade technical research.

## 🛠 Technical Stack

- **Frontend:** Modern HTML5, CSS3 (using custom variables for theming), and vanilla JavaScript.
- **Typography:** Professional serif (Lora) and sans‑serif (DM Sans) pairings for high readability.
- **Libraries:**
  - **Highlight.js:** Syntax highlighting for code outputs.
  - **Mermaid.js:** Rendering architectural diagrams.
  - **PDF.js & Mammoth:** Parsing uploaded documents and research papers.
- **Backend:** Powered by Cloudflare Workers (e.g., `*.vishwajeetadkine705.workers.dev` endpoints).

## 🎨 UI/UX Features

- **Mode‑Specific Interfaces:** Each active agent features a tailored UI with distinct color themes and specialized prompts.
- **Report System:** Agents generate structured, interactive reports with “Health Scores” and critical flags.
- **Interactive Workspaces:** Real‑time “Thinking” states and action cards provide feedback during complex AI tasks.
- **Multi‑Modal Exports:** Support for downloading insights as JSON, PDF, or copying to clipboard.

## 📂 Project Structure

```plaintext
├── index.html            # Main workspace launcher
├── dataset-builder.html  # Dataset Builder Agent
├── Research.html         # Research & Math Agent
├── Code-agent.html       # Code Agent
├── product.html          # Product Builder Agent
└── automation.html       # Automation Builder Agent
```

## 🚦 Getting Started

- **Deployment:** The workspace is built as a static frontend that interacts with Cloudflare Worker backends. Simply host the HTML files on any static hosting provider.
- **API Configuration:** Update the `BACKEND` constants in the `<script>` sections of the HTML files to point to your specific AI service endpoints.
- **Usage:** Open the specific HTML file for the agent you want, or use `index.html` to launch the five active agents from one place.
