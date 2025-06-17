# Preface: this project summary and the code involved are still a work in progress. The initial project was to explore movie review datasets using classic lexicon-based sentiment analysis and newer, transformer-based NLP models. The work and conclusions are briefly summarized below. The purpose of the refactoring and reorganizing the project codebase is for further exploration of the differences in applied use-cases for lexicon library vs transformer based analysis of short text samples like movie reviews. I will be further extending the project in my free time going forward as I explore NLP use cases for industry. 

Sentiment Analysis & Movie-Success Modeling  
Rotten Tomatoes + TMDb, 106 k reviews, 16 variables

### Why this repo exists
Two goals drive the work:

1. Compare a lightweight lexicon model (VADER) with a transformer model (DistilBERT via Flair) on sentiment-classification speed, accuracy, and interpretability.  
2. Trace how numeric, categorical, and text features of movie reviews translate into simple success proxies—revenue and average rating—through a transparent, reproducible pipeline.

The notebooks are broken up so a reader can jump straight to the part that matters:

01_eda.ipynb exploratory stats & plots
02_feature_eng.ipynb cleaning + engineered columns
03_modeling.ipynb baseline → tuned models, error analysis

### Data sources
* Rotten Tomatoes critics’ reviews (ratings, text, dates)  
* The Movie Database (TMDb) metadata (budget, revenue, runtime, cast, genres)  
Both dumps were merged on title + year after manual spot-checks for duplicates.

### Research design in one line
Clean → engineer text & categorical features → run sentiment analysis → visualise → model revenue / rating as dependent variables → interpret.

Key steps:

* **Prune noise** – drop rows with > 50 % missing cells (-319 rows).  
* **Impute** – median fill on the rest (all high-skew numeric cols).  
* **Standardise reviewer ratings** – map letter grades and X / Y ratios onto -1…1. Three helper functions (Convert_Grade, Convert_Scale, Convert_Date) catch 99 % of formats.  
* **Engineer** – split the genre list into `genre_1…genre_3`; extract `month` from release date.  
* Result: 106 318 rows × 16 well-named columns ready for analysis.

### EDA highlights

| variable   | shape                     | why it matters                        |
|------------|--------------------------|---------------------------------------|
| budget     | heavy right skew; outliers like *Endgame* | proxy for studio confidence and spend |
| runtime    | roughly normal           | interpretable lever for producers     |
| vote_count | extreme right skew       | indicates audience reach              |

Correlations that guided feature choice:

* `revenue` vs `budget` ≈ 0.79  
* `vote_average` vs `vote_count` ≈ 0.34  

Both pairs later show up as top signals in the regression models.

### Text → sentiment
* VADER (rule-based) – fast, transparent, no GPU.  
* Flair DistilBERT – context-aware, 250 MB download, slower on CPU.

VADER’s compound score tracked the reviewers’ own numeric ratings more closely, so the column derived from VADER is what flows into the downstream models.

Example:

```python
# VADER
{'neg': 0.12, 'neu': 0.71, 'pos': 0.17, 'compound': 0.34}

# Flair
[POSITIVE (confidence: 0.97)]
```
Modeling snapshot
Baselines: ordinary least squares for revenue, logistic + k-NN for vote_average buckets.

Feature set: numeric skims (log-scaled where needed), one-hot genres, month, VADER score.

Early result: adding VADER lifts revenue-RMSE by ~4 %, vote-F1 by ~6 % versus numeric-only baselines. Full discussion and error dives live in Phase 4.ipynb.

Re-running the pipeline
```bash
Copy
Edit
# create and activate env
uv venv .venv --python 3.12
source .venv/bin/activate
uv pip install -r requirements.txt

# first-time model downloads
python - <<'PY'
import nltk, flair
nltk.download('vader_lexicon')     # ~1 MB
# flair downloads automatically at first call
PY
To pre-fetch the DistilBERT weights manually, drop the file into
~/.flair/models/en-sentiment/ as noted in the notebooks.
```
Takeaways
Speed vs nuance – VADER is fine for dashboards; transformers win when sarcasm or idioms matter.

Budget still rules – bigger spend correlates with higher returns, but watch diminishing gains beyond the median.

Vote dynamics – quantity (votes) partly predicts quality (average), hinting at social-proof loops.

Clean first, question later – consistent column names and typed data saved hours once the modeling started.