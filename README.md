# GRPO-Based Fine-Tuning Pipeline for Cybersecurity Policy Generation

This repository contains a notebook-based pipeline for retrieval, completion generation, ranking, GRPO fine-tuning, evaluation, and multi-agent orchestration for cybersecurity policy generation.

The project is designed to be reproducible across macOS, Windows, and Linux.

---

## Project Overview

This workflow is organized into six notebook-based steps:

1. **Step 1 — Weaviate Indexing**  
   Build the retrieval corpus by reading source PDFs, chunking text, and storing embedded chunks in Weaviate.

2. **Step 2 — Completion Generation**  
   Generate multiple candidate cybersecurity policy completions per prompt.

3. **Step 3 — Completion Ranking**  
   Rank generated completions using a judge model and rubric-based scoring.

4. **Step 4 — GRPO Fine-Tuning**  
   Fine-tune the base model using grouped ranked completions.

5. **Step 5 — Base Model Evaluation**  
   Compute evaluation metrics from ranked outputs.

6. **Step 6 — Multi-Agent Workflow**  
   Run a CrewAI-based multi-agent cybersecurity policy generation workflow.

---

## Repository Structure


grpo-cybersec-project/
├── .env
├── README.md
├── SETUP_GUIDE.md
├── requirements.txt
├── notebooks/
│   ├── 01_Step1_Weaviate.ipynb
│   ├── 02_Step2_completions_v3.ipynb
│   ├── 03_step3_rank_completions_v3.ipynb
│   ├── 04_step4_GRPO_Finetuning.ipynb
│   ├── 05_step5_Base_Model_Evaluation.ipynb
│   └── 06_step6_MAIN_CyberSec_CrewAI_5Agents.ipynb
├── data/
│   ├── corpus/
│   ├── processed/
│   └── sample/
└── outputs/
    ├── completions/
    ├── rankings/
    ├── models/
    └── evaluations/


---

## Required Environment Variables

Create a file named `.env` in the project root and add:


OPENAI_API_KEY=your_openai_key
HF_TOKEN=your_huggingface_token
WEAVIATE_URL=your_weaviate_cluster_url
WEAVIATE_API_KEY=your_weaviate_api_key


Notes:
- `.env` is a hidden file on macOS/Linux.
- The Weaviate **cluster name** is not used in the code.
- Only `WEAVIATE_URL` and `WEAVIATE_API_KEY` are required by the notebooks.

---

## Data Layout

Place your source PDF corpus inside:

data/corpus/


Example:

data/corpus/
├── policy_1.pdf
├── policy_2.pdf
└── policy_3.pdf


Folder purposes:
- `data/corpus/` → original PDF corpus
- `data/processed/` → intermediate processed files
- `data/sample/` → optional sample data
- `outputs/completions/` → generated completions
- `outputs/rankings/` → ranked completions
- `outputs/models/` → trained checkpoints
- `outputs/evaluations/` → evaluation outputs

---

## Notebook Execution Order

Run the notebooks in this order:

1. `01_Step1_Weaviate.ipynb`
2. `02_Step2_completions_v3.ipynb`
3. `03_step3_rank_completions_v3.ipynb`
4. `04_step4_GRPO_Finetuning.ipynb`
5. `05_step5_Base_Model_Evaluation.ipynb`
6. `06_step6_MAIN_CyberSec_CrewAI_5Agents.ipynb`

---

## Quick Start

1. Clone or download the repository.
2. Create a Python virtual environment.
3. Install dependencies from `requirements.txt`.
4. Create the `.env` file in the project root.
5. Add your API credentials to `.env`.
6. Place your PDF corpus in `data/corpus/`.
7. Start Jupyter and run the notebooks in order.

For full setup instructions, see **`SETUP_GUIDE.md`**.

---

## Important Notes

- Run the notebooks from the project root directory.
- Do not hardcode local file paths such as `/Users/...`, `C:\...`, or `/content/...`.
- Do not hardcode API keys inside notebooks.
- Clear notebook outputs before sharing.
- The first code cell in each notebook should load `.env` and define the project paths.

---

## Expected External Services

This project depends on:
- **Weaviate Cloud** for vector storage and retrieval
- **Hugging Face** for model access
- **OpenAI** for judge-model-based ranking and some downstream agent workflows

---

## Reproducibility Notes

This project uses:
- relative paths through `Path`
- environment variables via `.env`
- notebook-specific setup cells
- standardized input and output folders

These choices make the repository portable across operating systems and easier to reproduce.

---

## Troubleshooting

For detailed troubleshooting and platform-specific setup instructions, see:

- `SETUP_GUIDE.md`

---

## Author

Ehsaneh Vilataj
