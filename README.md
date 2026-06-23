# WTA Match Predictor

A model that predicts the winner of women's pro tennis (WTA) matches from pre-match information only: ranking, recent form, surface history, and head-to-head. It reaches about 0.69 AUC on matches it hasn't seen, a bit better than simply picking the higher-ranked player.

The model itself is a logistic regression. The care went into the evaluation, since that's where these projects usually go wrong. Every feature is built from a player's earlier matches only, the train/test split is by date (fit on older matches, test on the most recent ones), and I judge it on AUC, log loss, and calibration rather than accuracy, which barely moves because ranking already calls most matches.

## Features
- Log ranking gap between the two players
- Recent form: win rate over the last 20 matches
- Surface win rate on hard, clay, and grass
- Head-to-head record

## Results
Trained on roughly 90,000 matches. The features above take AUC from 0.689 (ranking only) to 0.694 and lower log loss, with the probabilities staying well calibrated. Accuracy comes out about even with the baseline, which makes sense: ranking already decides most matches, so the gain is in the probability estimates, not the win/loss call. Surface win rate was the most useful addition. Recent form adds almost nothing once ranking is in.

## Running it
One notebook, `WTA_Match_Predictor.ipynb`. You'll need a free Kaggle account and an API token (`kaggle.json`) to pull the data; the notebook asks you to upload it. To run locally:

```
pip install -r requirements.txt
```

then run the notebook top to bottom.

## Data
Jeff Sackmann's tennis database, used under CC BY-NC-SA 4.0.
