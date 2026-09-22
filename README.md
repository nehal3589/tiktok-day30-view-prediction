# TikTok Day-30 View Prediction

## Project Overview

A predictive modeling project developed for a TikTok view prediction competition.

The goal is to predict the cumulative number of views a video will reach by Day 30 (`target_day30_views`) using information available during the first five days after publication.

The project uses video metadata, early engagement data, and historical creator statistics to build a regression model.

---

## Problem Statement

The objective is to predict the Day-30 cumulative views of TikTok videos based only on historical information available during the early stage of each video's lifecycle.

The available data includes:

- Video metadata
- Daily engagement statistics
- Daily creator statistics
- Engagement information from Day 0 to Day 5

The competition evaluates predictions using Root Mean Squared Error (RMSE).

---

## Data

The project uses the following competition-provided datasets:

- `train_videos.csv`
- `test_videos.csv`
- `engagement_daily.csv`
- `creators_daily.csv`
- `sample_submission.csv`

The original competition datasets are not included in this repository.

---

## Feature Engineering

The project creates features from the available video, engagement, and creator data.

### Video Features

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

### Day-5 Engagement Features

Engagement information available on Day 5 is used to extract:

- Day-5 views
- Day-5 likes
- Day-5 comments
- Day-5 shares
- Day-5 collects
- Day-5 downloads
- Day-5 WhatsApp shares

### Engagement Summary Features

Engagement data from Day 0 through Day 5 is summarized using:

- Mean views
- Maximum views
- Standard deviation of views
- Mean likes
- Mean comments
- Mean shares
- Mean collects
- Mean downloads
- Mean WhatsApp shares

### Growth Features

Early view growth is represented using:

- Day-0 views
- Day-5 views
- Day-0 to Day-5 view growth
- View growth ratio

### Interaction Features

The project calculates Day-5 engagement-to-view ratios:

- Like/View ratio
- Comment/View ratio
- Share/View ratio
- Collect/View ratio
- Download/View ratio
- WhatsApp Share/View ratio

### Creator Historical Features

Historical creator information available during the video's early period is used to create:

- Mean follower count
- Maximum follower count
- Mean following count
- Mean total favorited
- Mean video count
- Enterprise verification status

---

## Data Leakage Prevention

Only information available during the early period of the video is used for feature engineering.

Engagement features are restricted to Days 0–5.

Creator statistics are also filtered to the period from the video's creation date through Day 5.

This prevents information from later periods from being used to predict Day-30 views.

---

## Model

Several regression approaches were explored during the project.

The final model used for the competition submission was:

**RandomForestRegressor with Poisson criterion**

### Final Configuration

```text
n_estimators = 500
max_depth = None
min_samples_leaf = 2
max_features = 0.7
criterion = "poisson"
random_state = 42
n_jobs = -1
