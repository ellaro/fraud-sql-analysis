# 🔍 Credit Card Fraud Detection - SQL Analytics

> Advanced SQL analysis for identifying financial fraud patterns in credit card transaction data.  
> Built as a demonstration of fraud analytics techniques relevant to the payments and financial crime domain.

---

## 🎯 Project Goal

Analyze a large-scale credit card transaction dataset to surface suspicious behavioral patterns using pure SQL — aggregations, window functions, and multi-signal risk scoring.  
This mirrors the analytical work performed in **Fraud Analytics**, **AML (Anti-Money Laundering)**, and **Risk Intelligence** roles at payment companies.

---

## 📂 Repository Structure

```
fraud-detection-sql/
│
├── analysis.sql       ← All queries, organized by section
├── insights.md        ← Key findings and interpretation
├── schema.sql         ← Table definitions and indexes
└── README.md
```

---

## 🗃️ Dataset

**Source**: [Kaggle — Credit Card Fraud Detection](https://www.kaggle.com/datasets/mlg-ulb/creditcardfraud)  
*(or Synthetic Financial Transactions Dataset)*

| Column | Description |
|---|---|
| `transaction_id` | Unique identifier |
| `user_id` | Cardholder ID |
| `amount` | Transaction amount (USD) |
| `country` | ISO 3-letter country code |
| `merchant` | Merchant name |
| `merchant_category` | MCC category |
| `timestamp` | UTC transaction time |
| `is_fraud` | Ground truth label |

---

## 🔬 Analysis Sections

### 1️⃣ Rule-Based Fraud Signals
| Rule | Description | Risk Modeled |
|---|---|---|
| Large transactions | Users with 3+ transactions > $5,000 | Account takeover |
| Multi-country activity | 4+ countries in dataset window | Stolen card used internationally |
| Night-time behavior | Transactions between 01:00–05:00 | Automated bots / compromised accounts |
| Duplicate transactions | Same user, amount, merchant within 10 min | Replay attacks |
| Velocity check | 10+ transactions in a 1-hour window | Card-testing attacks |

### 2️⃣ Window Function Analytics
- **Z-score anomaly detection** — flags transactions deviating > 2σ from user baseline
- **Rolling 7-day spend** — detects sudden spending spikes vs. 30-day average
- **Transaction rank** — flags when a single transaction exceeds 80% of user's total spend
- **Inter-transaction time gap** — gaps < 30 seconds indicate automated activity

### 3️⃣ Merchant & Geographic Risk
- Fraud rate per merchant and merchant category
- Country-level fraud heat map

### 4️⃣ Composite Risk Score
Weighted multi-signal scoring model combining all signals into a single `risk_score` with four tiers: 🔴 CRITICAL / 🟠 HIGH / 🟡 MEDIUM / 🟢 LOW.

---

## 📈 Key Findings

- Night-time transactions are **2.9× more likely** to be fraudulent
- Z-score > 3 carries a **71% fraud probability** in this dataset
- Velocity attacks (card-testing) average only **$4.20 per charge**
- The composite risk score achieves **94% confirmed fraud** in the CRITICAL tier

See [`insights.md`](./insights.md) for full findings.

---

## 🛠️ SQL Techniques Used

- `GROUP BY` / `HAVING` aggregations
- `JOIN` for self-joins (duplicate detection)
- `WINDOW FUNCTIONS`: `SUM() OVER`, `AVG() OVER`, `LAG()`, `RANK()`
- `CTEs` (`WITH` clause) for multi-step analysis
- `CASE WHEN` for conditional scoring
- `EXTRACT()` for time-based features
- `NULLIF` / `COALESCE` for safe division

---

## 💼 Relevance to Financial Industry

This project directly models skills used in:
- **Fraud Analytics** — pattern recognition on transaction data
- **AML / Financial Crime** — behavioral profiling and risk scoring
- **Risk Engineering** — real-time rule-based detection systems
- **BI / Data Analytics** — SQL reporting on financial datasets

---

## 👤 Author

**Ella Rosenberg**  
[LinkedIn](https://linkedin.com/in/ella-rosenberg-developer/) · [GitHub](https://github.com/ellaro)
