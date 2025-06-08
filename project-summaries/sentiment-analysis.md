## Note on Sentiment Models

This project uses two sentiment analysis tools that require model downloads:

- **NLTK VADER**: Requires downloading the `vader_lexicon` on first use (~1MB)
- **Flair `en-sentiment`**: Downloads a pretrained DistilBERT model (~250MB) the first time it's used. Model will be cached locally (e.g., `~/.flair`).

➡️ Expect ~1GB of disk usage in total after setup, including dependencies.

You can download required resources by running:
```python
import nltk
nltk.download('vader_lexicon')

Flair will automatically download the en-sentiment model when called for the first time. The Flair API is very slow so you can download it ahead of time here

## ⚡ Faster Setup (Optional)

To avoid long model downloads via the Flair API (which can be very slow),
you can download the sentiment model manually here:

👉 [Download Flair en-sentiment (.pt)](https://nlp.informatik.hu-berlin.de/resources/models/sentiment-curated-distilbert/sentiment-en-mix-distillbert_4.pt)

Then place it in:

```bash
~/.flair/models/en-sentiment/sentiment-en-mix-distillbert_4.pt


NEW DIRECTION OF PROJECT

# 🧠 Sentiment Analysis with BERT vs. VADER  
*A Comparative Study Using Movie Review Data*

This project explores the application of **natural language processing (NLP)** for sentiment analysis using two distinct approaches:

- **Transformer-based model** (BERT via the Flair NLP framework)
- **Lexicon-based model** (VADER from NLTK)

The goal is to evaluate and compare the strengths and limitations of each method using a dataset of movie reviews, offering a practical demonstration of how modern deep learning models differ from traditional rule-based systems.

---

## ✨ Motivation

Sentiment analysis is a cornerstone of modern NLP, with applications in product reviews, social media monitoring, and customer feedback. While large pretrained models like **BERT** offer state-of-the-art accuracy, classic approaches like **VADER** remain attractive due to their speed and simplicity.

This project aims to:

- **Contrast accuracy and inference time** between both methods  
- Understand the tradeoffs between **deep learning models and lexicon heuristics**  
- Showcase **real-world application** of AI models to text classification problems

---

## 🔍 Models Used

### 🧠 **BERT-based Sentiment Analysis via Flair**
- Implemented using the [Flair NLP](https://github.com/flairNLP/flair) framework
- Backed by a fine-tuned DistilBERT sentiment model
- Offers contextual understanding of text
- **Requires model download (~250MB)** at first run

> Output: Confidence score and predicted label embedded in a `Sentence` object

---

### ⚡ **VADER (Valence Aware Dictionary for sEntiment Reasoning)**
- Rule-based sentiment analyzer from the [NLTK](https://www.nltk.org/) library
- Uses a curated lexicon of sentiment words and scoring rules
- Lightweight and fast, no model training required
- Performs surprisingly well on social media and short review text

> Output: Compound score and proportions of positive/neutral/negative tone

---

## 📊 What This Project Includes

- Jupyter notebook to:
  - Load and preprocess movie review data
  - Run both sentiment analysis pipelines
  - Compare predicted sentiments
  - Visualize distributions and mismatches
- Clean Python structure for reproducibility
- Optional Flair model downloader script for faster setup
- Commentary on strengths, weaknesses, and edge cases

---

## 📦 Installation

```bash
# Set up environment (recommended using uv or pip)
uv venv .venv --python 3.12
source .venv/bin/activate
uv pip install -r requirements.txt


SAMPLE OUTPUT
# VADER
{'neg': 0.123, 'neu': 0.711, 'pos': 0.166, 'compound': 0.34}

# BERT via Flair
[POSITIVE (confidence: 0.97)]


Observations (Discussed in Notebook)
Flair/BERT is more nuanced and handles sarcasm or context better

VADER is faster and sufficient for well-formed, literal sentences

Flair requires external model download and GPU acceleration for scale

Great teaching example for classical vs deep learning NLP

References
Flair NLP GitHub

VADER: Hutto & Gilbert (2014)

---


DEEPER DIVE
# 🤖 Lexicon-Based vs. Transformer-Based Sentiment Analysis  
*A Deeper Comparison of VADER and BERT in Applied NLP*

## 🧠 Overview

This project compares two fundamentally different approaches to sentiment analysis:

- **VADER**: A rule-based, lexicon-driven analyzer designed for fast, interpretable results  
- **Flair (DistilBERT)**: A deep neural model leveraging transformers and contextual embeddings

Though both aim to classify sentiment, they differ dramatically in how they interpret language. This comparison not only reveals their respective strengths and weaknesses, but also serves as a case study in choosing the right AI tools for different real-world applications.

---

## ⚙️ How Each Method Works

### 1. **VADER** (Valence Aware Dictionary for Sentiment Reasoning)
- **Mechanism**: Uses a fixed dictionary of ~7,500 words rated for sentiment, with rules for intensity (e.g., exclamation marks), degree modifiers (e.g., “very”), and negation (e.g., “not good”)
- **Design**: Tailored for **social media and short text** (e.g., tweets, reviews)
- **Output**: 4 scores (positive, neutral, negative, and a composite “compound” score)

> 🟢 **Advantages**:  
- Fast (sub-millisecond inference)  
- Interpretable — you can trace the score to specific words  
- No model download or training needed  

> 🔴 **Limitations**:  
- Cannot interpret context or semantics (e.g., sarcasm, negation scope)  
- Doesn’t adapt to domain-specific slang or idioms  
- Not robust to multi-clause or complex sentences  

---

### 2. **Flair with DistilBERT (Transformer-Based Model)**  
- **Mechanism**: Uses the BERT architecture, trained on large corpora to understand **semantic context** by processing all words simultaneously in self-attention blocks
- **Design**: The `en-sentiment` model is fine-tuned on labeled sentiment data
- **Output**: A class label (`POSITIVE` or `NEGATIVE`) with a confidence score

> 🟢 **Advantages**:  
- Understands **contextual relationships** between words  
- Handles multi-sentence reviews, idioms, and nuanced language  
- Adaptable to different domains via fine-tuning  

> 🔴 **Limitations**:  
- Heavier — requires downloading >250MB of model weights  
- Slower inference and higher memory usage  
- Less transparent ("black-box") predictions  

---

## 🧪 Observed Differences in This Project

| Case Type                   | VADER                          | Flair / BERT                     |
|----------------------------|--------------------------------|----------------------------------|
| Simple phrases             | ✅ Accurate                    | ✅ Accurate                      |
| “Not bad at all”           | ❌ Misclassified as negative   | ✅ Correctly inferred positive   |
| “I hated how good it was”  | ❌ Broken logic                | ✅ Understood contrast/sarcasm   |
| Slang or idioms (“mid”)    | ❌ Not in lexicon              | ✅ BERT adapts via embeddings    |
| Emojis / punctuation       | ✅ Integrated handling         | ❌ Lacks native emoji handling   |
| Speed                      | ⚡ Instant                     | 🐢 Slower (especially on CPU)    |

---

## 💡 Implications in Applied AI

This experiment illustrates a broader decision point in applied machine learning:

### ⚖️ Tradeoff: *Simplicity vs. Power*

- **Lexicon methods** like VADER are ideal for:
  - Real-time applications
  - Low-resource environments
  - High interpretability needs

- **Transformer models** like BERT are ideal for:
  - Complex, ambiguous, or domain-specific language
  - Applications where **accuracy outweighs latency**
  - Long-form review understanding and nuance detection

---

## 🧠 Why This Matters in Practice

| Application | Best Approach | Why |
|-------------|----------------|-----|
| Social media monitoring | **VADER** or hybrid | Fast, interpretable, domain-trained |
| Customer support tickets | **BERT** | Handles long messages, subtleties |
| News article tone | **BERT** | Needs contextual awareness |
| Embedded devices | **VADER** | Lightweight, no inference engine |
| Feedback dashboards | Depends | VADER for real-time; BERT for post-hoc analytics |

---

## 🧰 Final Thoughts

This project is more than a sentiment classifier — it’s an illustration of how **AI models are tools**, and the choice of model is as strategic as it is technical.

In a world where compute costs, interpretability, and latency matter just as much as accuracy, it's essential to understand the *philosophy and behavior* of our models — not just their performance metrics.

> ✅ **VADER** is the scalpel — precise, fast, and lightweight.  
> 🤖 **BERT** is the MRI — powerful, nuanced, and heavy.  
> Choosing the right one depends on the job.

---
