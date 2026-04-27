# The Vanishing All-Rounder
## Did the IPL's Impact Player Rule Reduce All-Rounder Use?

> **TL;DR:** Using unsupervised learning on 127,655 IPL deliveries (2018–2025), we find that the Impact Player rule significantly reduced genuine all-rounder deployment — league-wide usage dropped from 1.42 → 1.16 all-rounders per match (p=0.0000). Bowling all-rounders continue contributing in both departments; batting all-rounders have been converted to specialist batters.

---

## 👉 Start here: [`notebooks/main_notebook.ipynb`](notebooks/main_notebook.ipynb)

## 🎥 Project Video: [https://www.youtube.com/watch?v=6ZIVNkGnFSY](https://www.youtube.com/watch?v=6ZIVNkGnFSY)

---

## Research Questions

**RQ1:** Has the Impact Player rule reduced the number of genuine all-rounders teams field per match?

**RQ2:** Among all-rounders who do play, has their dual contribution pattern shifted post-2023?

---

## Results Summary

| Analysis | Metric | Finding | Significance |
|---|---|---|---|
| League AR count | Avg ARs/match | 1.42 → 1.16 (−0.26) | p=0.0000 ✓ |
| Batting contribution | GMM bat score | +0.050 increase | p=0.013 ✓ |
| Bowling contribution | GMM bowl score | −0.055 decline | p=0.173 (directional) |
| Dual deployment | DCI | −0.017 decline | p=0.034 ✓ |
| Quadrant shift | Batting AR % | 24.9% → 35.6% | +10.7pp |
| Team level | 6 of 10 teams | Fewer ARs post-IP | — |

**Key finding:** The Impact Player rule has bifurcated the all-rounder into two sub-types. Bowling all-rounders (Jadeja, Narine, Russell) continue contributing in both departments. Batting all-rounders (Tewatia, Samad, Dube) have been converted to specialist batters — their bowling replaced by the IP substitution mechanism.

---

## Data

**Source:** [Cricsheet.org](https://cricsheet.org) — IPL ball-by-ball JSON files

**Download:** Visit https://cricsheet.org/downloads/ and download the IPL JSON zip. Extract the JSON files into a folder and update `DATA_FOLDER` in the notebook:

```python
DATA_FOLDER = '/content/drive/MyDrive/ipl_json'  # update to your path
```

**Dataset stats:**
- 533 matches, 127,655 deliveries
- Seasons: 2018–2025 (8 seasons)
- Pre-Impact era: 314 matches (2018–2022)
- Post-Impact era: 219 matches (2023–2025)

> **Note:** Raw data files are not committed to this repo. Download from Cricsheet and point `DATA_FOLDER` to your local or Drive path before running.

**Preprocessing:** All preprocessing is done inline in `main_notebook.ipynb` — no separate scripts required.

---

## How to Reproduce

This project was built in **Google Colab (Python 3.12.13)**.

1. Clone the repo:
```bash
git clone https://github.com/Aakarsh2000/cric-analysis
```

2. Open `notebooks/main_notebook.ipynb` in Google Colab

3. Upload the Cricsheet IPL JSON files to your Google Drive and update `DATA_FOLDER` in cell 1

4. Run all cells top to bottom — each section is self-contained and builds on the previous

5. To install dependencies locally:
```bash
pip install -r requirements.txt
```

---

## Key Dependencies

| Package | Version | Purpose |
|---|---|---|
| Python | 3.12.13 | Runtime |
| pandas | 2.2.0 | Data manipulation |
| numpy | 1.26.0 | Numerical computing |
| scikit-learn | 1.4.1 | K-Means, GMM, Hierarchical clustering, PCA |
| scipy | 1.12.0 | Mann-Whitney U, Kruskal-Wallis tests |
| matplotlib | 3.8.0 | Static visualisations |
| plotly | 5.18.0 | Interactive scatter plots |

Full dependency list in [`requirements.txt`](requirements.txt).

---

## Repo Structure

```
cric-analysis/
│
├── notebooks/
│   └── main_notebook.ipynb                    # 👉 Main deliverable — start here
│
├── checkpoints/
│   ├── EDA_cricket_ball_by_ball_data.ipynb    # Checkpoint 1 — EDA
│   └── RQFormation.ipynb                      # Checkpoint 2 — RQ Formation
│
├── requirements.txt                           # Full Python environment
└── README.md
```

---

## Methodology Overview

1. **Data Loading** — Parse Cricsheet ball-by-ball JSON, compute `runs_bowler`, `is_legal`, phase labels
2. **Player-Season Statistics** — 25 batting and bowling features per player per season including phase-wise breakdowns
3. **Player Classification** — K-Means + GMM + Hierarchical clustering on career averages → majority vote → Pure Batter / Pure Bowler / All-Rounder (239 eligible players, 59 all-rounders)
4. **GMM Contribution Scores** — Separate batting and bowling GMMs on role-specific subpopulations → percentile-ranked scores per season
5. **Dual Contribution Index (DCI)** — Geometric product of batting and bowling percentile ranks → direct measure of genuine dual deployment
6. **Match-Level Classification** — Refit GMM + Hierarchical on 25 match-level features → season role via majority vote → count all-rounders per match per team
7. **Statistical Testing** — Mann-Whitney U (pre vs post), Kruskal-Wallis (three-period), Cohen's d effect sizes

---

## Collaboration Declaration

**Data Source:** Cricsheet.org — IPL ball-by-ball JSON files (2018–2025)  
**AI Tools:** Claude (Anthropic) — code generation, debugging, analysis design  
**Course:** CSCE 676 — Data Mining and Analysis, Texas A&M University
