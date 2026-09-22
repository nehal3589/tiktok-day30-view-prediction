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

# Feature Engineering

The model uses features derived from the video metadata, early engagement behavior, and creator history.

## 1. Video Metadata

The following video-level features are used:

- Duration
- Video resolution
- English language indicator
- AI-generated indicator
- Advertisement indicator
- Word count
- Emoji count
- Question count
- Hashtag count
- Speaking rate
- Emotion-related features
- Creation hour
- Creation weekday

The original resolution field was converted into a numeric feature before modeling.

---

## 2. Day-5 Engagement Features

The latest available engagement values at Day 5 were extracted:

- Day-5 views
- Day-5 likes
- Day-5 comments
- Day-5 shares
- Day-5 collects
- Day-5 downloads
- Day-5 WhatsApp shares

Day 5 was used as an important early indicator of how a video was performing before the Day-30 target period.

---

## 3. Engagement Summary Features

Engagement observations from Day 0 through Day 5 were summarized using:

- Mean views
- Maximum views
- Standard deviation of views
- Mean likes
- Mean comments
- Mean shares
- Mean collects
- Mean downloads
- Mean WhatsApp shares

These features capture the overall engagement behavior during the first six days.

---

## 4. Early Growth Features

To capture how quickly a video gained views, the project calculated:

- Day-0 views
- Day-5 views
- Day-0 to Day-5 view growth
- View growth ratio

The growth ratio provides a measure of the change in views relative to the initial Day-0 views.

---

## 5. Interaction Features

Engagement-to-view ratios were calculated using Day-5 engagement:

- Like/View ratio
- Comment/View ratio
- Share/View ratio
- Collect/View ratio
- Download/View ratio
- WhatsApp Share/View ratio

These features capture the relationship between views and different forms of user engagement.

---

## 6. Historical Creator Features

Creator statistics were calculated using information available during the video's early period.

The following features were created:

- Mean follower count
- Maximum follower count
- Mean following count
- Mean total favorited
- Mean video count
- Enterprise verification status

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
