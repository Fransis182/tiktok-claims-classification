# TikTok Project — Global Summary (Courses 1–6)

## Overview
This project focused on helping TikTok classify whether a video contains a **claim** or an **opinion** in order to support moderation prioritization and reduce review backlog.

---

## Course 1 — Project Proposal + Initial Inspection

### What was done
- Loaded `tiktok_dataset.csv`
- Reviewed shape, columns, data types, and descriptive statistics
- Checked missing values and label distribution
- Defined the business problem and initial approach

### Key findings
- Dataset size: **19,382 rows × 12 columns**
- Missing data: **298 rows**
- Class balance after cleaning:
  - **claim:** 50.35%
  - **opinion:** 49.65%
- Engagement variables appeared highly skewed with large outliers

---

## Course 2 — Exploratory Data Analysis

### What was done
- Explored distributions of views, likes, shares, comments, and downloads
- Created visualizations
- Reviewed outliers and correlation structure
- Engineered additional engagement-related features
- Compared patterns by `claim_status`

### Key findings
- Engagement variables were heavily right-skewed
- Strong correlation across engagement metrics
- Claim videos tended to receive higher reach and stronger engagement patterns
- Data quality issues and extreme values needed consideration before modeling

---

## Course 3 — Statistical Testing

### Research question
Is there a statistically significant difference in video views between verified and not verified accounts?

### Method
- Two-sample t-test
- Group variable: `verified_status`
- Outcome variable: `video_view_count`

### Results
- Mean views, not verified: **265,663**
- Mean views, verified: **91,439**
- t-statistic: **-25.49**
- p-value: **2.6e-120**

### Interpretation
There is a statistically significant difference in views between verified and not verified accounts.  
In this dataset, unverified accounts received more views on average.

---

## Course 4 — Logistic Regression

### What was done
- Cleaned and prepared the data
- Created `transcription_length`
- Encoded categorical variables
- Balanced the `verified_status` target
- Trained logistic regression
- Evaluated with confusion matrix and classification metrics

### Key findings
- Verified-related patterns were associated with longer content and more comments
- Performance was acceptable as a baseline but not as strong as the final claim-classification model
- This stage was useful for understanding how account and engagement variables interact

---

## Course 5 — Final Machine Learning Model

### Objective
Predict whether a TikTok video is a **claim** or an **opinion**.

### What was done
- Engineered `text_length`
- Prepared encoded feature matrix
- Split data into train / validation / test sets
- Tuned Random Forest and XGBoost using GridSearchCV
- Selected champion model based on recall and precision

### Results

#### Random Forest
- Recall: **0.9860**
- Precision: **1.0000**

#### XGBoost
- Recall: **0.9860**
- Precision: **0.9992**

### Champion model
**Random Forest**

### Test confusion matrix
- TN = **1895**
- FP = **0**
- FN = **17**
- TP = **1905**

### Feature importance
Top predictors:
1. `video_like_count`
2. `video_view_count`

This shows that engagement intensity was the strongest signal for claim detection in this dataset.

---

## Course 6 — Communication and Stakeholder Readout

### What was done
- Prepared final interpretation for technical and non-technical audiences
- Summarized strengths, limitations, and ethical implications
- Converted findings into stakeholder recommendations

### Main recommendation
Use the final model as a **decision-support tool** for moderation prioritization, while keeping human review in the workflow.

---

## Final conclusion
This was a full end-to-end analytics and machine learning portfolio project.  
It demonstrates:
- business framing,
- data exploration,
- statistical inference,
- baseline modeling,
- final machine learning,
- and executive communication.

The final model performed extremely well, but because the dataset is synthetic and the use case is moderation-related, deployment decisions should still include human oversight and further validation.
