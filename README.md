# Undergrad

This project demonstrates a full sentiment analysis pipeline on a dataset of movie reviews.  
We apply natural language processing (NLP) techniques to classify reviews as positive or negative.

## How to run using uv

```bash
uv venv .venv --python 3.12
source .venv/bin/activate
uv pip install -r requirements.txt
jupyter notebook notebooks/movie-sentiment-analysis.ipynb
```

## Project Structure
```bash
notebooks/     # Exploratory notebooks (contains main.ipynb)
src/           # Python modules (to be created during refactor)
artifacts/     # Saved models, metrics, outputs
data/          # Link to get dataset
```

