# TikTok Project — Global PACE

## PLAN

### Business objective
Build analytics and machine learning tools that help TikTok identify whether a video contains a **claim** or an **opinion** so content review can be prioritized more efficiently.

### Key questions
- What patterns separate claims from opinions?
- Which variables are most useful for classification?
- Can a model help reduce moderation backlog without creating unacceptable risk?
- What metrics matter most for this use case?

### Success criteria
Because missing a true claim is more harmful than reviewing an extra opinion, **recall for the claim class** is especially important.  
Precision also matters, because too many false positives would reduce operational efficiency.

### Ethical considerations
- False negatives may allow claim content to avoid timely review
- False positives may increase moderator workload
- The model should support moderation, not replace human judgment

---

## ANALYZE

### Data understanding
- Reviewed data structure, missingness, and class balance
- Identified 298 rows with missing values
- Observed near-balanced target distribution after cleaning

### Exploratory analysis
- Reviewed distributions of engagement variables
- Detected heavy right skew and extreme values
- Evaluated relationships across views, likes, shares, downloads, and comments
- Compared engagement patterns between claims and opinions

### Statistical analysis
- Conducted a two-sample t-test to compare video views across verified and not verified accounts
- Found a statistically significant difference

### Main analytical findings
- Engagement metrics are highly informative
- Claim videos tend to spread differently from opinion videos
- Several variables are strongly correlated and require careful interpretation

---

## CONSTRUCT

### Data preparation
- Removed incomplete rows
- Engineered `text_length`
- Encoded target and categorical variables
- Built train / validation / test sets

### Modeling
- Used logistic regression earlier in the project as a baseline modeling stage
- Built and tuned:
  - Random Forest
  - XGBoost

### Model selection logic
The final selection process prioritized:
1. Recall
2. Precision
3. Validation performance consistency
4. Business usefulness

### Final model
Random Forest was selected as the champion model.

---

## EXECUTE

### Final results
**Random Forest**
- Recall: **0.9860**
- Precision: **1.0000**

**XGBoost**
- Recall: **0.9860**
- Precision: **0.9992**

### Test performance of champion model
- TN = **1895**
- FP = **0**
- FN = **17**
- TP = **1905**

### Interpretation
The final model is highly effective at distinguishing claims from opinions in this dataset.  
It can help moderation teams prioritize review queues more efficiently.

### Recommendation
Proceed with the model as a **decision-support tool**, with:
- human review for flagged content,
- further validation on real-world data,
- monitoring for drift and fairness issues.

### Next steps
- Test the model on production-like data
- Add richer NLP features
- Explore calibration or confidence scoring
- Build downstream review rules for high-risk or high-reach videos
