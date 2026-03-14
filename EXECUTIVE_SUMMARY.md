# Executive Summary — TikTok Claims Classification

## Objective
Develop a predictive model that helps TikTok identify whether a video contains a **claim** or an **opinion** so moderation teams can prioritize review more efficiently.

## Business context
TikTok receives many user reports related to possible claims in videos.  
A reliable classification model can reduce backlog and improve review speed by helping moderators focus first on the most relevant content.

## Work completed
Across the project lifecycle, the analysis included:
- initial data inspection,
- exploratory data analysis,
- statistical testing,
- baseline modeling,
- final machine learning model development,
- and stakeholder-oriented interpretation.

## Final model
Two models were developed and compared:
- **Random Forest**
- **XGBoost**

Both models performed extremely well.  
**Random Forest** was selected as the champion model because it matched XGBoost on recall and performed slightly better on precision.

## Final results
### Cross-validation
**Random Forest**
- Recall: **0.9860**
- Precision: **1.0000**

**XGBoost**
- Recall: **0.9860**
- Precision: **0.9992**

### Test set
- TN = **1895**
- FP = **0**
- FN = **17**
- TP = **1905**

This means the final model:
- produced **no false positives** in the test sample,
- missed only **17 true claims**,
- and achieved near-perfect overall performance.

## Most important predictors
The strongest features were:
1. `video_like_count`
2. `video_view_count`

This suggests that engagement intensity is the strongest signal separating claims from opinions in this dataset.

## Benefits
- Faster prioritization of videos for review
- Reduced moderation backlog
- Strong predictive performance
- Clear business value as a support tool

## Limitations
- Dataset is synthetic
- Real-world performance may differ
- Moderation decisions are high-impact and require careful deployment

## Ethical considerations
The model should be used as a **decision-support tool**, not a fully automated moderation system.

Potential risks:
- False negatives may delay review of true claims
- False positives may create unnecessary moderator workload

Human review should remain part of the workflow.

## Recommendation
Proceed with this model for moderation prioritization support, while:
- keeping human review in place,
- validating on real-world data,
- and monitoring model behavior over time.
