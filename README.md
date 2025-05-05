
---

# Compound V2 Wallet Credit Scoring – Zeru Finance Challenge

## Overview

This repository contains a complete solution to the Zeru Finance challenge for scoring wallets on the Compound V2 protocol using only raw transaction data. The goal is to assign a credit score between 0 and 100 for each wallet address, where a higher score indicates more trustworthy and responsible financial behavior.

The problem is approached using custom feature engineering, behavioral analysis, and a rule-based scoring model that reflects protocol-specific dynamics.

---

## Repository Structure

```
.
├── Files/
│   ├── top_1000_accounts.csv
│   ├── bottom_1000_accounts.csv
│   ├── methodology.pdf
│   ├── wallet_analysis.pdf
├── notebook/
│   ├── wallet.ipynb
├── README.md
```

---

## Dataset

The raw dataset used for this project comes from Compound V2 protocol transaction logs, made available by Zeru Finance. You can access the dataset from the following Google Drive folder:

**[Compound V2 Raw Dataset – Google Drive](https://drive.google.com/drive/folders/1Xt9eJ-cFGGbJsmk5SsKFUrYDjIpmYcRY?usp=sharing)**

For this challenge, we selected the three largest files in the folder to cover a significant portion of protocol activity. These files were used to extract wallet-level behavior data including deposits, borrows, repays, liquidations, etc.

---

## Project Goals

* Build a credit scoring system without any external labels or pretrained models.
* Engineer meaningful features from raw transaction logs that reflect wallet behavior.
* Create a scoring model that is robust, explainable, and protocol-specific.
* Deliver scores for all wallets and export the top 1,000 and bottom 1,000 by score.

---

## Feature Engineering

Features were derived using time-series aggregation and behavior analysis from transaction logs. Key features include:

* `net_deposit_usd`
* `net_borrow_usd`
* `active_days`
* `total_volume_usd`
* `deposit_to_borrow_ratio`
* `repay_ratio`
* `liquidation_rate`

These features were normalized and weighted based on domain insights about responsible financial behavior.

---

## Scoring Model

A rule-based scoring mechanism was implemented using a weighted sum of scaled features:

* Each feature was scaled using Min-Max normalization.
* Weights were assigned to reflect importance (e.g., positive weights to deposits and repayment ratios; negative to liquidations).
* A final score between 0 and 100 was computed for every wallet.

Wallets were labeled as:

* `2` → Highly Trustable (Score ≥ 80)
* `1` → Medium Trust (Score ≥ 50 and < 80)
* `0` → High Risk (Score < 50)

---

## Deliverables

###  Methodology Document

Located at `Files/methodology.pdf`. It explains:

* The reasoning behind feature selection
* Scoring approach and normalization logic
* Justification for score interpretation

### Wallet Analysis

Located at `Files/wallet_analysis.pdf`. It includes:

* Detailed review of 5 high-scoring and 5 low-scoring wallets
* Observed behavioral patterns
* Risk/reliability interpretation based on transaction data

###  CSV Output

* `top_1000_accounts.csv`: Top 1000 wallets by score (sorted descending)
* `bottom_1000_accounts.csv`: Lowest 1000 wallets by score

---

## Instructions to Run

1. Clone the repository
2. Navigate to the `notebook/` directory
3. Open and run `compound_credit_scoring.ipynb` in Jupyter or any compatible environment
4. Make sure to load the selected raw dataset files locally from the Google Drive folder

---

## Requirements

Install the necessary Python packages:

```bash
pip install pandas numpy scikit-learn matplotlib seaborn
```

---

## License

This project is intended for the Zeru Finance credit scoring challenge and is not licensed for commercial use.

---


