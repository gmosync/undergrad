# Undergradate Coursework

This repository contains selected projects from my undergraduate studies in Business Analytics and Data Science. 

Each project is summarized in the [`project-summaries/`](./project-summaries/) folder. Only one of these projects, the [`sentiment-analysis/`](./sentiment-analysis/), uses publicly available data and includes full code, notebooks, and outputs.

The remaining projects were completed in partnership with my university and a major tech company, and involve confidential datasets. While the code and data cannot be shared, I’ve provided detailed markdown summaries to explain each project, also in the [`project-summaries/`](./project-summaries/) folder.

Below are quick summaries of each project:

[`predict-retention/`](./predict-retention/)
Partnering with the Office of Institutional Research & Effectiveness at my university, I linked first-year NSSE responses to four-year retention data with logistic regression on a cleaned sample of 2017 entrants. First-year GPA and the “Would you attend again?” survey item overshadowed all other factors, and reliance on informal advisors predicted non-retention. Findings helped justify hiring full-time professional advisors for first-year and undeclared students. Data and code remain private under confidentiality agreement.

[`predict-admissions/`](./predict-admissions/)
Using 15,000 historical admits and 69 features, I tested six classifiers and found logistic regression gave the best yield signal (Kappa 0.552). Early-decision status, top-percent-in-class, campus visits, and recruiter engagement dominated prediction, while test scores and broad demographics were weaker. Variable-importance and VIF checks kept the model interpretable. Data and code remain private under confidentiality agreement.

[`predict-supplychain/`](./predict-supplychain/)
I modeled in-transit lead times for a global tech OEM using six months of order data and a multivariable linear regression that explained 85.6 percent of the variance. Ship mode proved the biggest lever, with ocean lanes far slower than air or ground, while origin-site and seasonal effects also mattered. Scenario testing showed how blending faster lanes with cheaper modes can shave several days on urgent shipments without busting freight budgets. Data and code remain private under confidentiality agreement.

[`sentiment-analysis/`](./sentiment-analysis/)
I combined Rotten Tomatoes reviews with TMDb metadata, cleaned 100,000 critic reviews, and compared lexicon-based VADER and transformer-based DistilBERT sentiment scorers. VADER aligned best with numeric ratings and, alongside budget and vote count, drove both revenue and rating models. The repo is public because the data is open, I've uploaded refactored code (work-in-progress) in the [`notebooks/`](./notebooks/) folder, and am expanding it with faster GPU pipelines and additional NLP experiments.

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

> Use a project-local virtual environment so this repo’s
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