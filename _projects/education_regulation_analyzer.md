---
layout: page
title: Education Regulation Impact Analyzer (ERIA)
description: An AI-powered NLP pipeline utilizing Large Language Models to simplify complex education policies into structured, actionable insights.
img: assets/img/projects/eria/summary_dashboard.png
importance: 2
category: Machine Learning & AI
---

### Real-World Problem
Education regulations issued by governing bodies (like UGC, AICTE, and the Ministry of Education) are typically dense, highly unstructured, and difficult to interpret quickly. Stakeholders often struggle to extract actionable insights regarding compliance, risks, and timelines. This project solves this by transforming unstructured regulatory PDFs into a structured, decision-ready intelligence dashboard using advanced Generative AI and NLP techniques.

### Inputs & Data
* **Source Format:** Unstructured PDF and HTML regulation documents.
* **Content:** Highly technical policy text, circulars, and historical amendments.
* **Extraction:** Automated ingestion using PyMuPDF to parse text, strip artifacts, and prepare clean corpuses for generative analysis.

### Tech Stack
* **Large Language Models:** Groq API (`llama-3.3-70b-versatile`) for the Core Analysis Layer
* **NLP & Zero-Shot Classification:** Hugging Face `facebook/bart-large-mnli`
* **Document Processing:** PyMuPDF (Text Extraction)
* **Application & UI:** Python, Streamlit
* **Output Standardization:** Strictly validated JSON parsing and generation

### Engineering Workflow
1. **Document Ingestion:** Raw PDFs are ingested, and raw text is extracted using PyMuPDF.
2. **Preprocessing & Chunking:** Text is cleaned, normalized, and semantically chunked to fit safely within the LLM context windows while preserving regulatory context.
3. **Layer 2 (Topic Classification):** A Hugging Face BART MNLI model runs zero-shot classification to tag the specific regulatory domain.
4. **Layer 1 (Generative Analysis):** The processed chunks are fed into the **Groq API** (`llama-3.3-70b-versatile`) using highly engineered prompts to perform stakeholder impact forecasting and risk detection.
5. **Post-Processing:** The LLM's raw text is strictly enforced into a predetermined JSON schema.
6. **Dashboard Rendering:** The structured JSON is routed to a Streamlit UI, breaking down insights into Summary, Stakeholders, Risks, Impact, and Timeline views.

<div class="row"><div class="col-sm mt-3 mt-md-0">{% include figure.liquid loading="eager" path="assets/img/projects/eria/system_architecture.png" title="ERIA System Architecture" class="img-fluid rounded z-depth-1" %}</div></div><div class="caption">The end-to-end NLP pipeline (PDF → PyMuPDF → Chunking → BART MNLI → Groq API → JSON → UI) translating raw regulatory PDFs into structured JSON intelligence.</div>

### Gen-AI & Prompt Engineering Techniques
To prevent hallucinations and ensure high-quality, professional outputs, several advanced LLM engineering techniques were implemented:
* **Strict JSON Schema Enforcement:** The system prompt forces the LLM to output exclusively in a deeply nested JSON schema, ensuring seamless integration with the Streamlit frontend.
* **Causal Reasoning Constraints:** Prompts were engineered to reject generic summaries (e.g., "skill development"). The model is explicitly instructed to generate insights using *cause-effect language*, ensuring it identifies systemic impacts rather than just repeating the text.
* **Length & Quality Guardrails:** The generation parameters strictly mandate minimum sentence lengths (12-15 words) and penalize bullet fragments to maintain a high standard of policy analysis.
* **Multi-Agent Simulation:** The prompt instructs the LLM to act as a "Policy Analyst" and systematically analyze the document through distinct lenses (Students, Faculty, Institutions, Administrators).

<div class="row"><div class="col-sm mt-3 mt-md-0">{% include figure.liquid loading="eager" path="assets/img/projects/eria/upload_processing.png" title="Pipeline Processing" class="img-fluid rounded z-depth-1" %}</div></div><div class="caption">Streamlit interface displaying the step-by-step document ingestion, chunking, and LLM inference pipeline.</div>

### Metrics & Performance
* **Pipeline Speed:** End-to-end processing of standard regulation PDFs (Ingestion to UI rendering) executes in 10–30 seconds.
* **Schema Adherence:** Achieved near-perfect adherence to the complex nested JSON output schema via strict system prompting.
* **Zero-Shot Accuracy:** Successfully categorized regulatory topics without the need for fine-tuning via the Hugging Face BART MNLI model.

<div class="row"><div class="col-sm mt-3 mt-md-0">{% include figure.liquid loading="eager" path="assets/img/projects/eria/summary_dashboard.png" title="Summary Dashboard" class="img-fluid rounded z-depth-1" %}</div></div><div class="caption">The final structured output rendered in the Streamlit UI, providing clear, categorized insights derived from the LLM.</div>

### Deployment/Inference
The application is deployed as a modular **Streamlit** dashboard. It features a stateful UI that caches document hashes to prevent redundant LLM API calls, minimizing token usage and costs. Users can instantly export the generated intelligence as a raw JSON payload or a neatly formatted PDF report for offline stakeholder distribution.

<div class="row"><div class="col-sm mt-3 mt-md-0">{% include figure.liquid loading="eager" path="assets/img/projects/eria/risk_impact_view.png" title="Risk & Impact Analysis" class="img-fluid rounded z-depth-1" %}</div></div><div class="caption">Detailed Risk and Impact views demonstrating the LLM's ability to infer cause-and-effect challenges from policy text.</div>
