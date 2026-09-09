# Association Rule Mining — Online Retail (Market Basket Analysis)

A Python project that mines transaction data from an online retail store to discover **which products are frequently bought together**, using the **Apriori algorithm**. This is the same technique behind Amazon's "Frequently bought together" and supermarket loyalty-card basket analysis.

---

## 1. What is Association Rule Mining?

**Association Rule Mining** is an unsupervised ML technique that finds relationships between items in large transactional datasets. It answers the question:

> *"If a customer buys item A, how likely are they to also buy item B?"*

It's the algorithm behind **Market Basket Analysis** — literally examining what's in each customer's shopping "basket" across thousands of transactions to find patterns.

**Real-world uses:**
- Amazon / e-commerce → "Frequently bought together", "Customers also bought"
- Supermarkets → product placement (put chips near soft drinks), loyalty offers
- Netflix/Spotify → "watched/listened together" content bundling
- Hospitals → symptom/diagnosis co-occurrence patterns

---

## 2. Key Concepts (the full theory)

An association rule is written as:

```
{Antecedent} → {Consequent}
e.g. {Bread} → {Butter}
```
Meaning: customers who buy **Bread** tend to also buy **Butter**.

Three metrics decide whether a rule is *strong* / worth acting on:

### a) Support
How frequently the itemset appears across **all** transactions.
```
Support(A) = (Transactions containing A) / (Total transactions)
```
- Tells you how "popular" or common that item/combo is.
- Low support = rare combination, might not be worth targeting.

### b) Confidence
Given that a customer bought A, how often did they also buy B?
```
Confidence(A → B) = Support(A and B) / Support(A)
```
- Measures the **reliability** of the rule.
- Confidence of 0.75 means: 75% of people who bought A also bought B.

### c) Lift
Compares confidence against B's overall popularity — tells you if A actually *causes* more B purchases, or if B is just popular anyway.
```
Lift(A → B) = Confidence(A → B) / Support(B)
```
| Lift value | Meaning |
|---|---|
| Lift > 1 | A and B are positively associated (buying A increases chance of buying B) — a **useful rule** |
| Lift = 1 | A and B are independent — buying A has no effect on B |
| Lift < 1 | A and B are negatively associated (buying A makes B less likely) |

**Lift is the most important metric** — high confidence alone can be misleading if B is just a very popular item bought by everyone anyway.

---

## 3. The Apriori Algorithm (how rules are actually generated)

Checking every possible combination of items is computationally explosive (with thousands of products, the combinations run into the billions). **Apriori** solves this efficiently using one key principle:

> **Apriori principle:** If an itemset is infrequent, all its supersets must also be infrequent. (If `{A}` is rare, `{A, B}` can't be common.)

This lets the algorithm prune the search space early instead of checking everything. Steps:

1. **Find frequent single items** — keep only items with support ≥ `min_support` threshold.
2. **Combine into pairs** — generate 2-item combinations from the surviving items, keep only those meeting `min_support`.
3. **Combine into triples**, and so on — repeat, growing the itemset size each round, discarding anything below the support threshold at every step.
4. **Generate rules** from the final frequent itemsets, and filter rules by a `min_threshold` on confidence (or lift).

This project uses the `mlxtend` library's `apriori()` and `association_rules()` functions to implement exactly this.

---

## 4. Dataset

**Source file:** `Online Retail.xlsx` (UK-based online retailer transaction log)

| Column | Description |
|---|---|
| `InvoiceNo` | Unique transaction/invoice ID |
| `StockCode` | Product code |
| `Description` | Product name |
| `Quantity` | Units purchased in that transaction |
| `InvoiceDate` | Date/time of purchase |
| `UnitPrice` | Price per unit |
| `CustomerID` | Customer identifier (has missing values) |
| `Country` | Country of the customer |

- **541,909** total transaction rows, **38** countries
- `Description` has 1,454 missing values; `CustomerID` has 135,080 missing values (dropped/not needed for this analysis)
- Two country subsets are analyzed separately (largest transaction volumes): **United Kingdom** (495,478 rows) and **Germany** (9,495 rows)

Output file: **`best_anticidents_consequents.csv`** — the generated UK association rules (antecedents, consequents, support, confidence, lift) exported from the notebook.

---

## 5. Project Workflow (matches the notebook sections)

1. **Import Necessary Libraries** — `pandas`, and `mlxtend` (installed via `!pip install mlxtend`)
2. **Import Dataset** — load `Online Retail.xlsx`
3. **Data Understanding** — shape, nulls, `describe()`, unique counts per column, transaction count per country
4. **Data Preparation (per country — UK, then Germany)**
   - Filter data to one country
   - Drop `CustomerID` (not needed for basket analysis)
   - Drop remaining missing values
   - **Pivot into a basket matrix**: rows = `InvoiceNo` (each transaction), columns = `Description` (each product), values = `Quantity` summed, missing → 0
   - **One-hot encode**: convert quantities into 0/1 (bought / not bought) — Apriori works on presence/absence, not exact quantity
5. **Data Mining**
   - `apriori(df, min_support=0.03, use_colnames=True)` → frequent itemsets meeting ≥3% support
   - `association_rules(df, min_threshold=0.02)` → generate rules from those itemsets
   - Export UK rules to `best_anticidents_consequents.csv`
6. **Repeat the full process for Germany** (2nd largest market by transaction count) as a comparison

---

## 6. Sample Results

**UK — example discovered rules:**
| Antecedent | Consequent |
|---|---|
| GREEN REGENCY TEACUP AND SAUCER | ROSES REGENCY TEACUP AND SAUCER |
| JUMBO BAG PINK POLKADOT | JUMBO BAG RED RETROSPOT |
| JUMBO STORAGE BAG SUKI | JUMBO BAG RED RETROSPOT |

**Germany — example discovered rules:**
| Antecedent | Consequent |
|---|---|
| POSTAGE | REGENCY CAKESTAND 3 TIER |
| 6 RIBBONS RUSTIC CHARM | ALARM CLOCK BAKELIKE PINK |
| ROUND SNACK BOXES SET OF4 WOODLAND | POSTAGE, WOODLAND CHARLOTTE BAG |

These matched item pairs/sets are the actionable output — e.g. for store layout, bundle deals, or "you may also like" recommendations.

---

## 7. Tech Stack

- **Python 3**
- **pandas** — data loading, cleaning, pivoting
- **mlxtend** (`frequent_patterns`: `apriori`, `association_rules`) — frequent itemset mining and rule generation

---

## 8. How to Run

```bash
pip install pandas mlxtend openpyxl
jupyter notebook "Association_Rules__Online_Retail_.ipynb"
```
Ensure `Online Retail.xlsx` is in the same folder as the notebook before running (`openpyxl` is required by pandas to read `.xlsx` files).

---

## 9. Notes & Limitations

- **`min_support=0.03`** means an itemset must appear in at least 3% of all transactions to be considered — this is a hand-picked threshold; lowering it finds more (but rarer/noisier) rules, raising it finds fewer but more common ones. Worth tuning based on catalog size.
- **`association_rules(min_threshold=0.02)`** filters on the **default metric (confidence)** at a low 0.02 threshold — quite permissive. In practice you'd typically also filter/sort the output by **lift** (not just confidence) to surface the most meaningful rules, since high confidence alone can be misleading.
- **The UK pivot table keeps a `sum` column-level label** (from `aggfunc=["sum"]`) baked into the itemsets — visible in the UK results as `(sum, PRODUCT NAME)`. The Germany version uses a plain pivot (no `aggfunc` list) and doesn't have this artifact — worth aligning both to the cleaner format.
- **Only UK and Germany are analyzed** (the two highest-transaction countries) — the same pipeline could be repeated for any other country in the dataset.
- **`best_anticidents_consequents.csv`** in this upload is currently empty — regenerate it by rerunning the notebook's `to_csv()` cell if you need the exported file.
- Apriori scales exponentially with the number of unique products; for very large catalogs, faster alternatives like **FP-Growth** (also available in `mlxtend`) are typically preferred.

---

## 10. Files in this Project

| File | Description |
|---|---|
| `Association_Rules__Online_Retail_.ipynb` | Main notebook with the full workflow (UK + Germany) |
| `Online Retail.xlsx` | Source transaction dataset (not included in this upload — required to rerun) |
| `best_anticidents_consequents.csv` | Exported UK association rules |
| `README.md` | This file |
