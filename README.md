# IPL Cricket Data Mining Analysis

## 📖 Overview

Data mining project analyzing IPL cricket matches using ball-by-ball event data. This project applies multiple data mining techniques including:

* **Frequent Itemsets & Association Rules**: Ball-outcome pattern discovery
* **Graph Mining**: Batsman-bowler interaction networks
* **Sequential Pattern Mining**: Temporal ball sequences
* **Anomaly Detection**: Unusual match events

## 📁 Dataset

**Source:** [Cricsheet IPL Ball-by-Ball Data](https://cricsheet.org/downloads/)

- 1,000+ IPL matches
- ~400,000+ ball-by-ball events
- License: Open Database License (ODbL)

## 🚀 Quick Start

```bash
git clone https://github.com/Aakarsh2000/cric-analysis.git
cd cric-analysis
jupyter notebook project_checkpoint1.ipynb
```

## 🔍 Key Findings

- Wicket events occur in only 4.97% of deliveries (class imbalance)
- Batsman-bowler network is 92.4% sparse
- Death overs average 9.77 runs/over vs middle overs at 7.75 runs/over
- Traditional support thresholds (>5%) miss meaningful cricket patterns

## 🎯 Research Questions

1. How do different support thresholds affect pattern quality?
2. Do sequential patterns reveal insights missed by unordered mining?
3. How do rules differ across powerplay, middle, and death overs?
4. Can graph features predict outcomes better than raw statistics?

## 📝 Citation

```
IPL Cricket Data Mining Analysis
Author: Aakarsh
GitHub: https://github.com/Aakarsh2000/cric-analysis
Data: Cricsheet.org
```

## 📄 License

Educational use only. Data from Cricsheet (ODbL license).