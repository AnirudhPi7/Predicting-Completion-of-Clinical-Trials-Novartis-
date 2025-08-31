# Predicting-Completion-of-Clinical-Trials-Novartis-

---

## Introduction
This project focused on building a predictive system to estimate whether a clinical trial would be completed or not using only information available at the trial design stage. The motivation was to provide actionable, explainable insights that help optimize trial planning and resource allocation. By combining structured data models with fine-tuned biomedical language models, the solution aimed to deliver predictions that were both accurate and interpretable, enabling sponsors and researchers to proactively identify at-risk trials.

---

## Background
Clinical trials are critical for bringing new therapies to patients, but a large proportion of trials fail to reach completion due to funding shortages, poor design, or recruitment challenges. Traditional risk assessments rely on manual review of protocol documents, which is slow and inconsistent. With the rise of advanced machine learning and large language models, it is possible to analyze structured and unstructured trial data at scale, uncovering patterns that predict early discontinuation. This project applied this paradigm to clinical trial planning, balancing predictive performance with explainability for scientific and regulatory stakeholders.

---

## Problem Statement
The core challenge was to predict trial completion status (Completed vs. Not Completed: Suspended, Withdrawn, or Terminated) at the time of trial design. The solution had to:

1. Use only pre-trial information (no post-trial leakage).
2. Handle both structured attributes (sponsors, funders, design, locations) and unstructured text fields (titles, conditions, summaries).
3. Provide interpretable recommendations so stakeholders could adjust trial design variables to improve success likelihood.

---

## Terminologies
- **XGBoost:** Gradient boosting algorithm applied to structured trial features.
- **BART / Bio-Clinical BERT:** Transformer models fine-tuned on clinical trial text fields.
- **S-Learner:** Causal inference framework used to estimate treatment effects of design/funding variables.
- **SHAP (SHapley Additive exPlanations):** Technique for feature attribution and interpretability. 

---

## Dataset
The dataset was derived from ClinicalTrials.gov, focusing exclusively on pre-trial attributes to avoid post-trial leakage. It consisted of hundreds of thousands of records across diverse disease categories. Structured features included sponsor type, funder, collaborator information, trial phase, enrollment size, and study design parameters, while unstructured fields covered study titles, conditions, outcomes, and summaries. Location-based attributes such as country and development level were also included. The target variable was binary: whether the trial was completed or not.

---

## Data Cleaning & Preparation
Data preparation involved excluding features with high missingness or post-trial relevance, such as adverse events or completion dates. Minor missing values were imputed statistically, while categorical fields such as sponsor and funder were standardized and grouped into consistent categories. Text fields were cleaned and preprocessed with tokenization and normalization, and additional NLP-based features such as word counts and sentence counts were generated. Together, this ensured that the dataset was both clean and aligned for modeling.

---

## Methodology
The solution pipeline combined multiple approaches. Structured data was modeled using XGBoost, which handled categorical and numerical features effectively. For textual data, Bio-Clinical BERT models were fine-tuned on study fields such as conditions, titles, and outcomes, while BART was applied for automated disease categorization. Trials were first clustered into major disease categories—Oncology, Infectious, and Others—so that models could specialize within each segment. Finally, an ensemble framework combined predictions from structured and unstructured models through majority voting, yielding more robust results. A causal inference layer using the S-Learner framework was then applied to estimate the effect of funding type, sponsorship, and collaboration on trial completion, controlling for confounders such as geography and disease type.

---

## Model Architecture
The architecture was designed in a modular fashion. The first layer was preprocessing, which handled data cleaning, feature engineering, and NLP transformations. The second layer involved separate modeling tracks: XGBoost for structured data and fine-tuned transformer models for text. The third layer aggregated outputs through an ensemble voting mechanism, while the fourth interpretability layer combined SHAP-based feature importance with causal effect estimates to provide actionable insights into trial design choices.
<img width="1292" height="634" alt="image" src="https://github.com/user-attachments/assets/48fa11e5-62e5-471f-93ae-8a5b367b725a" />

---

## Results & Discussion
The ensemble model achieved an AUC-ROC of 0.65, outperforming individual base models. It demonstrated high precision in identifying completed trials, meaning that its positive predictions could be trusted with confidence. At the same time, it showed strong recall for not completed trials, which is crucial for flagging high-risk designs. SHAP analysis highlighted the importance of sponsor type, funding source, collaborator count, and disease category, while causal inference quantified how specific variables such as industry funding and international collaboration increased completion likelihood. Despite these successes, challenges remained, particularly in correctly classifying rare disease trials and trials from regions with diverse reporting practices such as the United States. Balancing recall and precision across categories also proved difficult, requiring threshold tuning.

---

## Conclusion & Future Scope
This project demonstrated that predicting trial completion at the design stage is not only feasible but also valuable for improving trial planning. By combining structured and unstructured modeling, ensemble learning, and causal inference, the system delivered both predictive accuracy and actionable recommendations. In future iterations, the model can be strengthened by incorporating more granular data, such as investigator experience and molecule-level characteristics, and by integrating advanced LLMs with richer embeddings to improve text understanding. Additional enhancements could include real-time monitoring of ongoing trials, scenario-based recommendation tools, and prescriptive analytics to proactively adjust trial design. Together, these steps would enable a more robust and adaptive decision-support system for clinical research stakeholders.

---

## Contributors
- Anirudh A
- Harsha P
- Kowshik M
- Moneesh B
- Yoogesh Kumar M

---
