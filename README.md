# World Cup 2026 Prediction Model

This repository presents a **data-driven approach to predicting the FIFA World Cup 2026**, combining historical match data, team strength ratings, and Poisson distribution theory to forecast scorelines, match outcomes, and the full tournament bracket. The analysis leverages **machine learning techniques** to model expected goals and translate them into calibrated win, draw, and loss probabilities.

---

## Project Context

The project was designed to predict **every match in the 2026 World Cup** — all 72 group stage fixtures and all 32 knockout matches — before a single ball was kicked, as part of a DataCamp prediction competition.

Rather than predicting scorelines directly, the model estimates each team's **expected goals** for a given matchup using XGBoost, then treats that figure as the λ (lambda) parameter of an independent Poisson distribution. This means scorelines, win/draw/loss probabilities, and both-teams-to-score probabilities are all derived **analytically** from the same underlying distribution rather than approximated through repeated simulation.

Key aspects of the analysis include:
- Using **XGBoost regressors** to predict each team's expected goals based on relative strength, form, and squad quality
- Applying **Elo rating-based scaling** to correct for mean-regression in tree-based models, sharpening predictions for clear mismatches
- Deriving scoreline and outcome probabilities **analytically from Poisson distributions**, rather than Monte Carlo simulation
- Simulating the **full knockout bracket** — group standings determine qualifiers, who are slotted into the Round of 32 per FIFA's official seeding rules, with results propagating through to the Final
- Validating the model against actual **2018 and 2022 World Cup** results to sanity-check winner accuracy and scoreline precision

The goal is to translate historical international football data into a **fully deterministic, reproducible tournament simulation**, while being transparent about where uncertainty in football genuinely limits predictability.

---

## What's Included
- `wc26_poisson.ipynb`: Full notebook — data loading, feature engineering, model training, validation, and tournament simulation
- `group_fixtures.csv`: WC 2026 group stage fixture list
- `knockout_slots.csv`: WC 2026 knockout bracket structure (Round of 32 → Final)
- `results.csv`: Historical international match results used for training
- `former_names.csv`: Historical country name changes for data normalisation
- `WC_Images`: group standings, knockout bracket results, and match probability reports

---

## Methodology Summary

| Stage | Approach |
|---|---|
| Feature engineering | Rolling 10-match form, Elo differentials, squad market value, tournament/recency-weighted historical data |
| Goal prediction | XGBoost regressors (home/away), trained on 9,600+ matches since 2010 |
| Scoreline derivation | Expected goals scaled by Elo gap, rounded to nearest integer |
| Outcome probabilities | Analytical Poisson — no simulation |
| Knockout tiebreaks | Win probability from joint Poisson distribution when rounding produces a draw |
| Validation | Backtested on WC 2018 and WC 2022 actual results |

---

## Results (Group Stage)

After all 72 group stage matches:
- **46/72** match outcomes correctly predicted (63.9%)
- **5** exact scorelines
- **27/32** knockout qualifiers correctly identified
- **6/12** groups predicted with perfect placement
- **92.5%** accuracy across all individual group placement predictions

---

## Tools Used
- **Python** (Pandas, NumPy, Matplotlib, SciPy, Scikit-learn, XGBoost)
---

## Future Work
Future updates will explore **head-to-head features for closely-matched rivalries, historical Elo trajectories to capture squad momentum, and context-dependent scoreline predictions** with richer event-level data, alongside continued validation as the knockout rounds are played.

---

## Contact
If you'd like to discuss football analytics, predictive modelling, or collaboration opportunities:
- [LinkedIn](https://www.linkedin.com/in/aaditpahuja)
- 📧 aaditpahuja@gmail.com
