# Undergradate Coursework

This repository contains selected projects from my undergraduate studies in Business Analytics and Data Science. 

Each project is summarized in the [`project-summaries/`](./project-summaries/) folder. Only one of these projects, the [`sentiment-analysis.md/`](./project-summaries/sentiment-analysis.md/), uses publicly available data and includes full code, notebooks, and outputs.

The remaining projects were completed in partnership with my university and a major tech company, and involve confidential datasets. While the code and data cannot be shared, I’ve provided detailed markdown summaries to explain each project, also in the [`project-summaries/`](./project-summaries/) folder.

---
## Project Summaries

[`predict-retention.md/`](./project-summaries/predict-retention.md/)
Partnering with the Office of Institutional Research & Effectiveness at my university, I linked first-year NSSE responses to four-year retention data with logistic regression on a cleaned sample of 2017 entrants. First-year GPA and the “Would you attend again?” survey item overshadowed all other factors, and reliance on informal advisors predicted non-retention. Findings helped justify hiring full-time professional advisors for first-year and undeclared students. Data and code remain private under confidentiality agreement.

[`predict-admissions.md/`](./project-summaries/predict-admissions.md/)
Using 15,000 historical admits and 69 features, I tested six classifiers and found logistic regression gave the best yield signal (Kappa 0.552). Early-decision status, top-percent-in-class, campus visits, and recruiter engagement dominated prediction, while test scores and broad demographics were weaker. Variable-importance and VIF checks kept the model interpretable. Data and code remain private under confidentiality agreement.

[`predict-supplychain.md/`](./project-summaries/predict-supplychain.md/)
I modeled in-transit lead times for a global tech OEM using six months of order data and a multivariable linear regression that explained 85.6 percent of the variance. Ship mode proved the biggest lever, with ocean lanes far slower than air or ground, while origin-site and seasonal effects also mattered. Scenario testing showed how blending faster lanes with cheaper modes can shave several days on urgent shipments without busting freight budgets. Data and code remain private under confidentiality agreement.

[`sentiment-analysis.md/`](./project-summaries/sentiment-analysis.md/)
I combined Rotten Tomatoes reviews with TMDb metadata, cleaned 100,000 critic reviews, and compared lexicon-based VADER and transformer-based DistilBERT sentiment scorers. VADER aligned best with numeric ratings and, alongside budget and vote count, drove both revenue and rating models. The repo is public because the data is open, I've uploaded refactored code (work-in-progress) in the [`notebooks/`](./notebooks/) folder, and am expanding it with faster GPU pipelines and additional NLP experiments.
