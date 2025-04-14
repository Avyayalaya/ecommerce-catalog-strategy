# 🔎 Search + Recommendations

This section addresses the two critical elements of Catalog Excellence:

1. **Eliminating failed searches** (removing the weak link)
2. **Delivering great alternatives** (strengthening the strong link)

Together, these systems ensure that customers always find something relevant—and often something better.

---

## 1. ❌ Weak Link: Eliminating Failed Searches

A failed search ("no results found" or irrelevant matches for specific terms) breaks user trust—especially when the query contains **clear intent** or a **proper noun** (e.g., brand names like “Nike”).

### A. Systematic Failed Search Program

**Core Idea**: Create a living map of failed searches and systematically close them.

#### Steps:
1. Collect the **top 5,000 queries per category** over a trailing 30–60 day period.
2. Identify queries with:
   - Zero results
   - Poor engagement (e.g., high bounce, no clicks)
3. Classify root causes:
   - Catalog gap
   - Search ranking failure
   - Typo / synonym / alias mismatch

### ✅ Example
- Query: `boAt Nirvana Ion earbuds`
- Result: “No results found” (due to missing listing)
- Fix: Identify from external sources → Match and prioritize for onboarding

### B. Automated Discovery & Matching

- For each failed query:
  - Run it through the flattened external catalog
  - Attempt title/brand-based matching using fuzzy search (e.g., Levenshtein, BM25, or vector similarity)
  - Rank matched external items by relevance and popularity

### C. Resolution Pipeline

- **If item is on external catalog but missing internally** → Candidate for onboarding
- **If item exists but doesn’t show up in results** → Search team reviews ranking + indexing
- **If it’s a synonym/variant (e.g., “sneakers” vs “running shoes”)** → Update query understanding engine

### D. Retail & Ops Interface

- Dashboards showing top unresolved queries
- Review tools that show side-by-side:
  - Failed query
  - Suggested match
  - Current catalog coverage

### ✅ Example
- Query: `Khadi Neem Soap`
- Suggested match: `Khadi Natural Herbal Neem Soap 125g`
- Issue: Item exists but not indexed under the correct synonym

---

## 2. 💡 Strong Link: Alternatives That Convert

When a user is still exploring, **surfacing the right alternatives** on search result pages (SERP) determines whether they stay, discover, and convert.

### A. Building the Recommendation Engine

**Goal**: Provide high-quality, intent-aligned alternatives before the user lands on a product page.

#### Input Signals:
- Brand proximity
- Price range
- Category overlap
- Glance views / impressions
- Add-to-cart and conversion data

#### Similarity Score Model:
A dynamic score for every product pair:
```
similarity_score = w1 * brand_similarity +
                   w2 * price_proximity +
                   w3 * shared_attributes +
                   w4 * engagement_overlap +
                   w5 * conversion_ratio_similarity
```

#### Predictive Edge Modeling:
To strengthen substitute recommendations:
- Train ML models (e.g., **XGBoost**) on product pair features:
  - Brand similarity, price difference, co-session frequency
  - Metadata alignment and conversion funnel similarity
- Output: High-confidence substitutes prioritized on SERP

### ✅ Example
- User searches: `wireless keyboard`
- Seen product: Logitech K230 Wireless Keyboard
- Alternatives shown:
  - Dell KM117 Wireless Keyboard (predicted substitute via XGBoost)
  - HP CS10 Combo

### B. Graph-Integrated Recommendations

Plug similarity scores and ML-predicted substitutes into the **product graph**:
- Use edges to recommend variants, substitutes
- Dynamically update edge weights based on real-time user signals

### ✅ Example
- Node A: Apple iPad Air 5th Gen
- Node B: Samsung Galaxy Tab S8
- Edge Type: Substitute (ML-predicted and reinforced by user co-view)

### C. Learning from Outcomes

- Measure **win ratio**: how often a recommended alternative is chosen over the original path
- Train the model to optimize for win ratio over clicks
- Include diversity constraints to avoid repetition

---

## 3. 🔁 Feedback Loops

- Capture false positives (bad recos) and missed intents via:
  - User feedback
  - Retail input
  - A/B tests

### ✅ Example
- Reco shown: “Apple Watch Band” as an alternative to “Samsung Galaxy Watch”
- Feedback: Retail marks this as irrelevant → Down-rank edge in graph

- Use this data to:
  - Adjust weights
  - Refine edge generation in product graph
  - Improve ranking logic

---

## ⚠️ Risks & Mitigations

| Risk                                 | Mitigation Approach                                        |
|--------------------------------------|-------------------------------------------------------------|
| Recos too similar to original        | Inject diversity constraints, control for novelty bias     |
| Good products buried in search       | Combine catalog + search telemetry to surface under-indexed SKUs |
| Query intent misclassified           | Use supervised intent modeling + synonym dictionaries       |
| Overload of suggestions              | Limit visible alternatives to high-confidence, high-impact ones |

---

## ✅ Outcome

A powerful feedback-driven loop between **Search**, **Recommendations**, and **Catalog** that:
- Closes high-signal gaps
- Surfaces meaningful alternatives (driven by predictive models)
- Keeps users engaged and discovering

> “Search is not a box. It’s a dialogue. Recos aren’t decoration. They’re decision support.”
