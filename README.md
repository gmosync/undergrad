# Undergradate Coursework

This repository contains selected projects from my undergraduate studies in **Business Analytics and Technology**, with a minor in **Data Science**. 

Each project is summarized in the [`project-summaries/`](./project-summaries/) folder. Only one of these projects — the **Movie Sentiment Analyzer** — uses publicly available data and includes full code, notebooks, and outputs.

The remaining projects were completed in partnership with university faculty and involve **confidential datasets**. While the code and data cannot be shared, I’ve provided detailed markdown summaries to explain each project’s scope, tools, and impact.

---

## Project Structure

```bash
undergrad/
├── .venv/ # local virtual environment (created using uv)
├── notebooks/ # Jupyter notebooks file for sentiment analysis project
├── src/ # Python modules and reusable code
├── data/ # local data files (ignored - check DATASETS.md for download)
├── artifacts/ # model outputs, plots
├── requirements.in # top-level dependencies
├── requirements.txt # fully pinned lock file (auto-generated)
└── .gitignore # files excluded
```

## Reproducing the environment

> **Recommended:** use a project-local virtual environment so this repo’s
> dependencies stay isolated from any other Python projects on your machine.

### Using `uv`

```bash
# 1. Clone the repo
git clone git@github.com:gmosync/undergrad.git
cd undergrad

# 2. Create a virtual environment (uv auto-creates .venv if not present)
uv venv

# 3. Install the exact pinned dependencies
uv pip install -r requirements.txt

# 4. Launch Jupyter
jupyter notebook
```
### Alternatively, using `venv` + `pip`

```bash
# 1  Clone the repo
git clone git@github.com:gmosync/undergrad.git
cd undergrad

# 2  Create & activate a virtual environment (Python ≥ 3.10)
python3 -m venv .venv
# macOS / Linux
source .venv/bin/activate
# Windows (PowerShell)
# .venv\Scripts\Activate.ps1

# 3  Install the exact pinned dependencies
pip install -r requirements.txt

# 4  Launch Jupyter
jupyter notebook
```