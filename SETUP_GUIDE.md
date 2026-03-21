# Setup Guide

This guide explains how to set up and run the project on macOS, Windows, or Linux.

---

# 1. Prerequisites

You need:

- Python 3.10 or 3.11
- Jupyter Notebook or JupyterLab
- Internet access
- A Weaviate Cloud cluster
- A Hugging Face token
- An OpenAI API key

Optional but recommended:
- GPU environment for faster fine-tuning

---

# 2. Clone or Download the Repository

If using Git:

```bash
git clone <your-repository-url>
cd grpo-cybersec-project
```

If using a ZIP file:
- Download the project
- Extract it
- Open a terminal inside the extracted project folder

---

# 3. Verify Project Folder

Your project root should contain:


README.md
SETUP_GUIDE.md
requirements.txt
notebooks/
data/
outputs/


You should run everything from this root folder.

---

# 4. Create the Data and Output Folders

If they do not already exist, create them.

## macOS / Linux

```bash
mkdir -p data/corpus data/processed data/sample outputs/completions outputs/rankings outputs/models outputs/evaluations
```

## Windows PowerShell

```powershell
mkdir data/corpus, data/processed, data/sample, outputs/completions, outputs/rankings, outputs/models, outputs/evaluations
```

---

# 5. Create a Virtual Environment

## macOS / Linux

```bash (could be optional name in case you already have this name)
python3 -m venv .venv
source .venv/bin/activate
```

## Windows Command Prompt

```cmd
python -m venv .venv
.venv\Scripts\activate
```

## Windows PowerShell

```powershell
python -m venv .venv
.venv\Scripts\Activate.ps1
```

---

# 6. Install Dependencies

After activating the environment:

```bash
pip install --upgrade pip
pip install -r requirements.txt
```

---

# 7. Create the `.env` File

Create a file named exactly:


.env


This file must be placed in the project root.

## macOS / Linux

```bash
touch .env
```

## Windows PowerShell

```powershell
New-Item .env -ItemType File
```

## Verify hidden file on macOS / Linux

```bash
ls -la
```

You should see `.env`.

---

# 8. Add Credentials to `.env`

Open `.env` and paste:

```env
OPENAI_API_KEY=your_openai_key
HF_TOKEN=your_huggingface_token
WEAVIATE_URL=your_weaviate_cluster_url
WEAVIATE_API_KEY=your_weaviate_api_key
```

Save the file.

---

# 9. How to Save and Exit in `nano`

If you open the file using:

```bash
nano .env
```

Then:

- Press `CTRL + O` to save
- Press `Enter` to confirm
- Press `CTRL + X` to exit

---

# 10. Create a Weaviate Cloud Cluster

This project requires an active Weaviate Cloud cluster.

## Steps

1. Go to the Weaviate Cloud Console
2. Create an account or sign in
3. Create a cluster
4. Copy:
   - cluster URL
   - API key
5. Paste them into `.env`

Important:
- The **cluster name** can be anything
- The cluster name is **not used** in the code
- Only the cluster URL and API key are required

No manual collection/schema setup is needed if Step 1 handles collection creation.

---

# 11. Add Your PDF Corpus

Put your source PDFs in: ('It's already there if you want to add more pdf files you can add it here ')

```text
data/corpus/
```

Example:

```text
data/corpus/
├── doc1.pdf
├── doc2.pdf
└── doc3.pdf
```

This folder is used by **Step 1**.

---

# 12. Start Jupyter

From the project root:

```bash
jupyter notebook
```

or

```bash
jupyter lab
```

Then open the notebooks from the `notebooks/` folder.

---

# 13. Run the Notebooks in Order

Run the following notebooks in sequence:

1. `01_Step1_Weaviate.ipynb`
2. `02_Step2_completions_v3.ipynb`
3. `03_step3_rank_completions_v3.ipynb`
4. `04_step4_GRPO_Finetuning.ipynb`
5. `05_step5_Base_Model_Evaluation.ipynb`
6. `06_step6_MAIN_CyberSec_CrewAI_5Agents.ipynb`

Do not skip earlier steps unless the required outputs already exist.

---

# 14. Common First Code Cell in Each Notebook

Each notebook should begin with a setup cell similar to this:

```python
import os
from pathlib import Path
from dotenv import load_dotenv

load_dotenv()

if Path.cwd().name == "notebooks":
    PROJECT_ROOT = Path.cwd().parent
else:
    PROJECT_ROOT = Path.cwd()

DATA_DIR = PROJECT_ROOT / "data"
CORPUS_DIR = DATA_DIR / "corpus"
PROCESSED_DIR = DATA_DIR / "processed"
SAMPLE_DIR = DATA_DIR / "sample"

OUTPUT_DIR = PROJECT_ROOT / "outputs"
COMPLETIONS_DIR = OUTPUT_DIR / "completions"
RANKINGS_DIR = OUTPUT_DIR / "rankings"
MODELS_DIR = OUTPUT_DIR / "models"
EVAL_DIR = OUTPUT_DIR / "evaluations"
```

Why this matters:
- it avoids machine-specific paths
- it works across operating systems
- it keeps the notebooks portable

---

# 15. Platform Notes

## macOS / Linux
- `.env` is hidden by default
- use `ls -la` to view hidden files

## Windows
- use PowerShell or Command Prompt
- if activation is blocked in PowerShell, run Command Prompt instead

---

# 16. Troubleshooting

## Problem: `.env` does not seem to load
Check:
- file name is exactly `.env`
- file is in the project root
- notebook is run from the repository folder
- `python-dotenv` is installed

## Problem: Notebook cannot find files
Check:
- PDFs are in `data/corpus/`
- notebook is run from the correct repository
- path definitions use `Path`, not hardcoded local paths

## Problem: Weaviate connection fails
Check:
- `WEAVIATE_URL` is correct
- `WEAVIATE_API_KEY` is correct
- cluster is active and reachable

## Problem: Hugging Face login fails
Check:
- `HF_TOKEN` is valid
- your Hugging Face account has access to the required model (you should request access if have not already done)

## Problem: OpenAI ranking fails
Check:
- `OPENAI_API_KEY` is valid
- your account has access to the required OpenAI model

## Problem: Notebook still uses `/content/...` or local machine paths
Replace those with relative project paths using `PROJECT_ROOT` and `Path`

---

# 17. Before Sharing the Repository

Before sending the project to others:

1. Clear all notebook outputs
2. Remove hardcoded keys
3. Remove hardcoded local file paths
4. Verify `.env` is not committed publicly
5. Make sure `requirements.txt` is up to date

Recommended:
- Restart kernel
- Clear output
- Save notebook

---

# 18. Recommended Sharing Notes for Colaborators


- create `.env` in the project root
- add their own keys
- place PDFs in `data/corpus/`
- create a Weaviate cluster before running Step 1
- run notebooks in order

---

# 19. Final Checklist

Before running the project, confirm:

- [ ] Python environment created
- [ ] Dependencies installed
- [ ] `.env` created
- [ ] OpenAI key added
- [ ] Hugging Face token added
- [ ] Weaviate URL added
- [ ] Weaviate API key added
- [ ] PDF corpus placed in `data/corpus/`
- [ ] Jupyter started from project root
- [ ] Notebooks run in order

---
