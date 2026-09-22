# TikTok Day-30 View Prediction

## Project Overview

This project was developed for a predictive modeling competition focused on predicting the cumulative number of views a TikTok video would reach by Day 30.

The model uses video metadata, early engagement data from Days 0–5, and historical creator statistics to predict `target_day30_views`.

---

## Problem Statement

The goal is to predict a video's Day-30 cumulative views using only information available during its early lifecycle.

The competition evaluates predictions using **Root Mean Squared Error (RMSE)**.

---

## Dataset

The competition provided:

- `train_videos.csv` — training video metadata and target
- `test_videos.csv` — test video metadata
- `engagement_daily.csv` — daily video engagement statistics
- `creators_daily.csv` — daily creator statistics

Dataset sizes:

- Training: 12,000 videos
- Test: 3,001 videos
- Engagement: 79,489 records
- Creators: 252,166 records

---

## Feature Engineering

The final feature set combines several types of information:

### Video Metadata
Features such as duration, aspect ratio, language, content indicators, word count, hashtags, speaking rate, emotions, and posting time.

### Early Engagement
Day-5 views and engagement metrics including likes, comments, shares, collects, downloads, and WhatsApp shares.

### Engagement Summary
Mean, maximum, and standard deviation of views and mean engagement statistics across Days 0–5.

### Growth Features
The change and growth ratio between Day-0 and Day-5 views.

### Interaction Ratios
Engagement-to-view ratios such as:

- Like / View
- Comment / View
- Share / View
- Collect / View
- Download / View
- WhatsApp Share / View

### Creator Features
Historical creator statistics including follower count, following count, total favorited, video count, and verification status.

The final dataset contained **48 numerical features**.

---

## Data Leakage Prevention

Engagement features were restricted to Days 0–5.

Creator statistics were also restricted to the period from the video's creation date through five days after posting.

No external data or information beyond the allowed observation period was used.

---

## Model

The final model is a **Random Forest Regressor with Poisson Criterion**.

### Final Configuration

```text
n_estimators = 500
max_depth = None
min_samples_leaf = 2
max_features = 0.7
criterion = "poisson"
random_state = 42
n_jobs = -1
```

---

## Cross-Validation

A 5-fold shuffled cross-validation strategy was used with `random_state=42`.

| Fold | RMSE |
|---|---:|
| 1 | 70,957.90 |
| 2 | 98,812.56 |
| 3 | 51,461.84 |
| 4 | 200,378.13 |
| 5 | 57,198.73 |
| **Mean** | **95,761.83** |

---

## Technologies

- Python
- Pandas
- NumPy
- Scikit-learn
- KaggleHub
- Google Colab

---

## Requirements

```text
pandas
numpy
scikit-learn
kagglehub
```

---

## Author

**Nehal Hamed Alzahrani**
