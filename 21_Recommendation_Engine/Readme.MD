# Movie Recommendation Engine — User-Based Collaborative Filtering (UBCF)

A Python/Pandas project that recommends movies to users by finding other users with similar taste and suggesting what they liked. This README explains what a recommendation engine is, the different types that exist, and exactly how this project's engine works.

---

## 1. What is a Recommendation Engine?

A **recommendation engine (recommender system)** is an algorithm that predicts what a user will like — a movie, product, song, etc. — based on data such as past ratings, purchases, or behavior. Instead of showing every user the same content, it personalizes results for each individual.

You interact with recommendation engines constantly:
- Netflix / Prime Video → "Because you watched..."
- Amazon → "Customers who bought this also bought..."
- Spotify → "Discover Weekly" playlist
- YouTube → suggested videos

**Goal:** predict a rating or preference score for items a user hasn't seen yet, then recommend the highest-predicted ones.

---

## 2. Types of Recommendation Engines

### a) Content-Based Filtering
Recommends items similar to what the user already liked, based on **item attributes** (genre, actors, keywords, description).
- Example: You liked a sci-fi movie → get recommended other sci-fi movies.
- Needs item metadata, not other users' data.
- Weakness: keeps recommending the "same type" of thing (limited diversity).

### b) Collaborative Filtering (CF)
Recommends items based on **patterns across users**, without needing to know anything about the item's content — only the rating/interaction matrix (user × item).

Two main sub-types:

| Type | Idea | Example |
|---|---|---|
| **User-Based CF (UBCF)** | Find users similar to *you*, recommend what *they* liked | "Users like you also enjoyed..." |
| **Item-Based CF (IBCF)** | Find items similar to what *you* liked, recommend those | "Because you rated X highly, try Y" |

- Strength: no item metadata needed — works purely from ratings.
- Weakness: **cold start** problem (new users/items with no ratings can't be handled well); struggles at large scale (computing similarity between millions of users is expensive).

### c) Hybrid Recommendation Systems
Combine content-based + collaborative filtering (and sometimes other signals like popularity, demographics) to get better accuracy and avoid the weaknesses of a single method. Netflix and Amazon use hybrid systems in production.

### d) Other approaches (for awareness)
- **Popularity-based**: recommend whatever is trending / most rated (no personalization).
- **Knowledge-based**: uses explicit rules/preferences (common in real estate, cars).
- **Model-based CF**: uses matrix factorization / ML models (e.g., SVD, ALS, deep learning) instead of direct similarity — scales better than plain UBCF/IBCF.

**This project implements User-Based Collaborative Filtering (UBCF)** — the "users like you" approach.

---

## 3. How UBCF Works (the logic used in this notebook)

UBCF works in 4 conceptual steps:

1. **Build a User–Item matrix** — rows = users, columns = movies, values = ratings (missing ratings filled with 0).
2. **Measure similarity between users** — compare each user's rating pattern to every other user's, using a similarity/distance metric.
3. **Find the nearest neighbors** — the most similar users to the target user.
4. **Recommend** — suggest movies that similar users rated highly but the target user hasn't watched yet.

The key design choice in UBCF is **which similarity metric** to use. This project builds and compares three:

| Metric | What it measures | Notebook usage |
|---|---|---|
| **Pearson Correlation** | How similarly two users' ratings *rise and fall* relative to their own average (pattern of preference, ignores rating scale bias) | `piv_table.corr()` |
| **Euclidean Distance** | Straight-line numeric distance between two users' rating vectors — **smaller = more similar** | `pairwise_distances(metric="euclidean")` |
| **Cosine Similarity** | Angle between two users' rating vectors — **closer to 1 = more similar**, ignores magnitude | `1 - pairwise_distances(metric="cosine")` |

> Note: Euclidean distance is a *distance* (lower = more similar), while Pearson correlation and cosine similarity are *similarity scores* (higher = more similar). Don't compare their raw values directly against each other.

---

## 4. Dataset

**File:** `Movie.csv`

| Column | Description |
|---|---|
| `userId` | Unique ID of the user who rated the movie |
| `movie` | Movie title (with release year) |
| `rating` | Rating given by that user (numeric, e.g. 0.5–5.0) |

- Rows: 8,992 rating records
- Unique users: 4,081
- No missing values
- This is "long format" data — one row per (user, movie, rating) — which gets **pivoted** into a wide user×movie matrix before similarity can be computed.

---

## 5. Project Workflow (matches the notebook sections)

1. **Import Necessary Libraries** — `pandas`, `sklearn.metrics.pairwise_distances`
2. **Import Dataset** — load `Movie.csv`
3. **Data Understanding** — check nulls, shape, unique users/movies
4. **Data Preparation & Model Building (Pearson)**
   - Pivot table: `index=movie, columns=userId, values=rating`, missing → 0
   - `piv_table.corr()` → user-to-user Pearson correlation matrix
5. **UBCF using Euclidean Distance**
   - Pivot table: `index=userId, columns=movie, values=rating`, missing → 0
   - `pairwise_distances(metric="euclidean")` → user-to-user distance matrix
6. **UBCF using Cosine Similarity**
   - Same pivoted matrix → `1 - pairwise_distances(metric="cosine")` → user-to-user similarity matrix
7. **Analysis / Validation**
   - Inspect the first 20 users' similarity/distance values
   - Manually cross-check: compare user `12` and user `23`'s actual movie ratings to sanity-check whether the computed similarity makes sense

---

## 6. Tech Stack

- **Python 3**
- **pandas** — data loading, pivoting, correlation
- **scikit-learn** (`sklearn.metrics.pairwise_distances`) — Euclidean & Cosine distance computation

---

## 7. How to Run

```bash
pip install pandas scikit-learn jupyter
jupyter notebook UBCF_Recommendation_Engine.ipynb
```
Ensure `Movie.csv` is in the same folder as the notebook before running.

---

## 8. Notes & Limitations

- **Filling missing ratings with 0** is a simplification — it can bias similarity scores, since "0" is treated as an actual low rating rather than "not rated." A common improvement is mean-centering ratings first, or using similarity metrics that naturally ignore unrated (NaN) entries.
- **No explicit "Top-N recommendation" output** is generated yet in the notebook — currently it computes and inspects similarity/distance matrices. The next step to complete an end-to-end recommender would be: pick a target user → find their top-K most similar users → aggregate/weight the movies those neighbors rated highly → exclude movies the target user already watched → output the ranked recommendation list.
- **Scalability**: UBCF recomputes similarity across *all* users, which becomes slow as user count grows into millions — in production this is usually replaced or supplemented with Item-Based CF or matrix-factorization (model-based) approaches.
- **Cold start**: a brand-new user with no ratings cannot get UBCF recommendations until they rate at least a few movies.
- Three similarity metrics are included so results can be compared — in practice, one metric is chosen based on which gives the most sensible/accurate recommendations for the given dataset.

---

## 9. Files in this Project

| File | Description |
|---|---|
| `UBCF_Recommendation_Engine.ipynb` | Main notebook with the full workflow |
| `Movie.csv` | Dataset of user movie ratings |
| `README.md` | This file |
