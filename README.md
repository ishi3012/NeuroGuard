# NeuroGuard 
![Build Status](https://img.shields.io/badge/build-passing-brightgreen.svg)
![Python Version](https://img.shields.io/badge/python-3.10+-blue.svg)
![License](https://img.shields.io/badge/license-MIT-blue.svg)
![Agent Framework](https://img.shields.io/badge/built_with-Vertex%20AI%20ADK-yellow.svg)
![Skills](https://img.shields.io/badge/skills-RAG%2FCoT%2FNLI%2FABSTAIN-blueviolet.svg)
![Status](https://img.shields.io/badge/status-MVP%20in%20progress-orange.svg)

> A Modular Agentic Framework for Hallucination Mitigation in LLMs using RAG, Chain-of-Thought, and NLI

**NeuroGuard** is a hybrid hallucination mitigation agent built using Google Cloud’s Vertex AI Agentic Development Kit (ADK). It integrates modular reasoning skills such as semantic retrieval (RAG), step-wise reasoning (CoT), factual verification (NLI), and abstention fallback logic to ensure LLM outputs are trustworthy and grounded.

## MVP Features

- **Retrieval-Augmented Generation (RAG)** using SBERT + FAISS
- **Chain-of-Thought Reasoning** via structured prompt chaining
- **Natural Language Inference (NLI)** for entailment-based hallucination detection
- **Abstention Logic** when answer confidence is low or ambiguous
- **Vertex AI ADK Agent** orchestration with YAML-defined skill flow

## System Architecture

```mermaid
flowchart TD
    A[User Question] --> B[RAG Skill (SBERT + FAISS)]
    B --> C[CoT Skill (Reasoning Prompt Builder)]
    C --> D[NLI Skill (Verifier Model)]
    D --> E[Fallback Skill (Threshold Logic)]
    E --> F{Confidence Sufficient?}
    F -->|Yes| G[✅ Final Answer]
    F -->|No| H[🛑 Abstention Response]
```

## Why Agentic AI?

NeuroGuard’s agentic architecture enables modular, explainable, and auditable reasoning — critical for hallucination-sensitive applications in healthcare, education, and enterprise knowledge delivery.

Tool-augmented decision chains like RAG → CoT → NLI → Fallback simulate how humans verify facts and build trust in multi-step reasoning.

## Tech Stack
| Layer              | Tools & Frameworks                                              |
|-------------------|------------------------------------------------------------------|
| Embeddings & Search | Sentence-BERT, FAISS                                           |
| Prompting & Reasoning | OpenAI GPT-4, Gemini, Chain-of-Thought Templates            |
| Verification       | NLI (via entailment models or LLM API)                         |
| Agent Framework    | Vertex AI Agentic Development Kit (ADK)                        |
| Interface (Planned)| Streamlit, FastAPI                                             |
| Deployment & Orchestration | Vertex AI, GCP, GitHub Actions                        |


## Directory Structure

``` bash
neuroguard/
├── neuroguard_agent/           # ADK-compliant agent logic
│   ├── main.py                 # Orchestrates skill calls
│   ├── agent.yaml              # Declares agent config and skills
│   ├── rag_skill.py            # Semantic retrieval skill
│   ├── cot_skill.py            # Chain-of-thought reasoning logic
│   ├── nli_skill.py            # Natural Language Inference logic
│   ├── fallback_skill.py       # Threshold-based abstention logic
├── configs/
│   └── base_config.yaml        # Thresholds, paths, etc.
├── data/
│   └── nutrition_kb.txt        # Domain-specific factual KB
├── scripts/
│   └── setup_env.sh            # Virtualenv + install script
├── tests/
│   └── test_rag_skill.py       # Unit tests for skills
├── requirements.txt
├── model_card.md               # (Optional) for model registry
├── LICENSE
└── README.md
```

## Getting Started

#### 1. Install dependencies
``` bash
bash scripts/setup_env.sh
```
#### 2. Run the Agent Locally
``` bash
python neuroguard_agent/main.py
```
#### 3. Test Individual Skills
``` bash
pytest tests/test_rag_skill.py
```
#### 4. [Planned] Launch Streamlit UI
``` bash
streamlit run interface/app.py
```

## Hallucination Handling Flow

- **If retrieval fails** → abstain

- **If CoT output is vague** → fallback logic triggers

- **If NLI contradicts retrieval** → return abstention response

- **If all checks pass** → return grounded answer

## Future Enhancements

### Reasoning:
- Toolformer-style reasoning for deeper validation
- Self-consistency prompting

### Interface:
- Streamlit dashboard to visualize CoT + NLI traces
- Human-in-the-loop override & feedback collection

### Deployment:
- Register agent in Vertex AI Agent Builder
- Serve via REST endpoint or as a Slack chatbot

## Author
**Shilpa Musale** – [LinkedIn](https://www.linkedin.com/in/shilpamusale) • [GitHub](https://github.com/ishi3012) • [Portfolio](https://ishi3012.github.io/ishi-ai/)

## 📄 License

This project is licensed under the [MIT License](LICENSE).

