# TikTok Claims Classification

End-to-end portfolio project completed as part of the **Google Advanced Data Analytics Certificate**.

This repository documents the full TikTok claims classification workflow across the project lifecycle: data inspection, exploratory data analysis, statistical testing, baseline modeling, final machine learning, and stakeholder communication.

---

## Business problem

TikTok users can report videos that may contain **claims**. Those reports create a large moderation backlog.  
The goal of this project is to support moderation teams by building analytics and machine learning tools that help distinguish between:

- **Claim**: information that is unsourced or comes from an unverified source
- **Opinion**: a personal belief, view, or thought

A reliable model can help prioritize videos for review more efficiently.

---

## Project objective

Build and evaluate models that classify TikTok videos as **claims** or **opinions** using available metadata, engagement metrics, account information, and text-derived features.

---

## Dataset

**Source file:** `tiktok_dataset.csv`  
**Rows:** 19,382  
**Columns:** 12  

Each row represents a published TikTok video.

### Core variables
- `claim_status`
- `video_id`
- `video_duration_sec`
- `video_transcription_text`
- `verified_status`
- `author_ban_status`
- `video_view_count`
- `video_like_count`
- `video_share_count`
- `video_download_count`
- `video_comment_count`

---

## Full project scope

### Course 1 — Project proposal and initial data inspection
Main work completed:
- Loaded and inspected the dataset
- Reviewed structure, data types, and descriptive statistics
- Identified missing values and class balance
- Framed the business problem and initial research direction

Key findings:
- Dataset is almost perfectly balanced between claims and opinions
- 298 rows contain missing values in `claim_status`, `video_transcription_text`, and engagement metrics
- Engagement variables show large spread and outliers

### Course 2 — Exploratory Data Analysis (EDA)
Main work completed:
- Explored variable distributions
- Created histograms and boxplots
- Analyzed correlations among engagement metrics
- Engineered engagement-rate style features
- Reviewed outliers and data quality issues

Key findings:
- Engagement variables are heavily right-skewed
- Likes, views, shares, downloads, and comments are strongly correlated
- Claim videos tend to generate higher engagement and stronger spread patterns than opinion videos

### Course 3 — Statistical testing
Main work completed:
- Defined a formal hypothesis test
- Compared video views between verified and not verified accounts
- Ran a two-sample t-test

Key findings:
- There is a statistically significant difference in mean views by `verified_status`
- Unverified accounts received more views on average in this sample
- Reach appears to be driven more by content dynamics than by verification alone

### Course 4 — Logistic regression modeling
Main work completed:
- Cleaned the data
- Created `transcription_length`
- Encoded categorical variables
- Addressed class imbalance in `verified_status`
- Trained and evaluated a logistic regression model

Key findings:
- Verified accounts were more likely to be associated with slightly longer videos, longer transcripts, and more comments
- The model detected verified users reasonably well, but performance was weaker for not verified accounts
- The stage was useful as a baseline modeling exercise

### Course 5 — Final machine learning model
Main work completed:
- Reframed the modeling task around **claim vs opinion**
- Built and compared **Random Forest** and **XGBoost**
- Used a train/validation/test workflow
- Tuned hyperparameters with cross-validation
- Selected the champion model based primarily on **recall**

Key findings:
- Both models performed extremely well
- **Random Forest** was selected as the final model
- The most predictive variables were:
  1. `video_like_count`
  2. `video_view_count`
- The final model achieved near-perfect performance on the test set

### Course 6 — Final communication and stakeholder delivery
Main work completed:
- Summarized findings for technical and non-technical audiences
- Prepared executive-style recommendations
- Framed benefits, limitations, ethical implications, and next steps

---

## Final modeling results

### Model comparison
**Random Forest**
- Recall: **0.9860**
- Precision: **1.0000**

**XGBoost**
- Recall: **0.9860**
- Precision: **0.9992**

### Champion model
**Random Forest** was selected because it matched XGBoost on recall and performed slightly better on precision.

### Test performance
- TN = **1895**
- FP = **0**
- FN = **17**
- TP = **1905**

Interpretation:
- No false positives in the test sample
- Very few missed claims
- Strong potential for moderation-prioritization support

---

## Most predictive features

Top feature importances from the champion model:

1. `video_like_count` → 0.4877  
2. `video_view_count` → 0.4399  
3. `video_share_count` → 0.0183  
4. `video_comment_count` → 0.0146  
5. `author_ban_status_banned` → 0.0110  
6. `text_length` → 0.0092  
7. `verified_status_verified` → 0.0066  
8. `video_download_count` → 0.0065  
9. `video_duration_sec` → 0.0064  
10. `author_ban_status_under review` → 0.0000  

The final model relied primarily on **engagement intensity**, especially likes and views.

---

## Business insights

- Claim videos tend to spread differently from opinion videos
- Engagement variables contain strong predictive signal
- Machine learning can help prioritize moderation queues efficiently
- Human review should still remain in the workflow for flagged or high-impact content

---

## Ethical considerations

This model should be used as a **decision-support tool**, not a fully automated moderation system.

Main risks:
- **False negatives** may allow harmful claim content to avoid priority review
- **False positives** may increase moderation workload

Because content moderation can have meaningful consequences, human oversight remains necessary.

---

## Repository contents

Recommended files for this repository:

- `README.md` → complete project overview
- `TikTok_Claims_Classification.ipynb` → final machine learning notebook
- `COURSE_SUMMARY.md` → global summary of all project stages
- `PACE_GLOBAL.md` → end-to-end PACE document
- `EXECUTIVE_SUMMARY.md` → stakeholder-oriented summary
- `requirements.txt`
- `.gitignore`
- `tiktok_dataset.csv`

---

## Tools used

- Python
- Pandas
- NumPy
- Matplotlib
- Seaborn
- Scikit-learn
- XGBoost
- Jupyter Notebook

---

## Conclusion

This project demonstrates a full analytics-to-modeling workflow for a content moderation use case.  
Across the full project, the data showed strong differences in engagement behavior between claims and opinions, and the final Random Forest model achieved excellent performance.

The project is valuable not only because of the final model, but because it shows complete analytical progression:
business framing, EDA, testing, baseline modeling, final modeling, and executive communication.
