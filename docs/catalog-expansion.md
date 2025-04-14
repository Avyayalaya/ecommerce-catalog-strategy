# 🛒 Catalog Expansion

Catalog expansion is the foundation of selection-led growth. It focuses on identifying and onboarding the **long-tail of products** that customers want but may not yet exist in the catalog. This process must be **programmatic**, **feedback-driven**, and **scalable** across millions of items.

---

## 1. 🔍 Identification & Extraction

Start small, but start right:
- Begin with the **Top 50 high-signal sources**: online retailers (e.g., Newegg for tech, iHerb for supplements), manufacturer listings, offline distributor catalogs, niche category sites.
- Set up a web scraping pipeline or API ingestion where possible.
- Normalize data: extract clean product titles, brand, specs, images, and pricing.

> 🚫 Do not scale beyond these 50 sources until the downstream systems (processing, matching, feedback) are stable and self-correcting.

### ✅ Example
- Source: iHerb supplement listings
- Extracted: Title: "Ashwagandha 600mg 90 capsules", Brand: Himalaya, Price: $12.99
- Normalize: Category = Supplements → Adaptogenic Herbs

---

## 2. 🧳️ Processing Pipeline

All extracted data is stored in a **flattened, normalized external catalog dataset**.

### Key steps:
- **Schema Design**: Unified schema across sources: fields like `title`, `brand`, `price`, `specifications`, `url`, `image_link`
- **Deduplication**: Identify duplicates using clustering based on brand-title-price
- **Normalization**: Translate product attributes to internal catalog taxonomy

---

## 3. 🔗 Product Graph Construction

A **Product Graph** represents relationships across items:
- **Nodes** = Products/SKUs
- **Edges** = Substitutes, Variants, Shared Specs, Cross-sells

### Example:
- Node A: "iPhone 14 128GB Blue"
- Node B: "iPhone 14 256GB Blue"
- Edge: Variant → same model, different specs

---

## 4. 🧠 Matching Engine

This is where the system identifies *true gaps* in the current catalog.

### Matching Approach:
- **Exact Match**: Title + brand + model alignment
- **Fuzzy Match**: Title similarity (e.g., cosine similarity on embeddings), price proximity
- **Graph-Based Match**: Match based on known edges (e.g., Samsung Galaxy A14 LTE → Edge exists with Samsung Galaxy A14 5G)

### Outcome Labels:
- ✅ Matched → Exists, no action needed
- ⚠️ Partial Match → Needs review (e.g., spec mismatch or alternate packaging)
- ❌ No Match → Candidate for onboarding

---

## 5. 📊 Prioritization & Scoring

Prioritize gaps using:
- Source popularity (e.g., rank on Amazon, Bestsellers tag)
- Brand authority (e.g., known top brands)
- Internal demand signals (e.g., past failed searches)

### Example Composite Score:
```
score = (0.4 * source_popularity_rank) + 
        (0.3 * brand_authority_score) + 
        (0.3 * frequency_in_failed_searches)
```

---

## 6. 🛠️ Internal Interfaces

Develop tooling for:
- **Retail Teams**: UI with filterable unmatched items + status tracker
- **Leadership Dashboards**: Coverage KPIs, ingestion velocity, gap closure rate

### Example Retail Use-Case:
- Retail manager sees: 18 unmatched SKUs in top 100 failed queries
- Clicks to onboard: 12 fast-tracked, 6 flagged for review

---

## 7. 🔁 Feedback Integration

- Capture corrections from retail teams (e.g., brand overrides, spec corrections)
- Integrate this feedback into:
  - Metadata inference models
  - Matching logic retraining
  - Source reliability scores

> ✅ Goal: Build a **self-improving system** where each human input improves the system for future inputs.

---

## 8. 👥 Team Structure

Create a cross-functional expansion pod:
- **Data Engineers**: Ingestion + ETL pipelines
- **ML Engineers**: Matching & scoring models
- **Technical PMs**: System design, adoption, backlog
- **Retail Ops**: Subject matter feedback + onboarding

This team must operate like a product team with iteration, feedback cycles, and fast resolution loops.

---

## ⚠️ Risks & Mitigations

| Risk                                 | Mitigation Approach                                        |
|--------------------------------------|-------------------------------------------------------------|
| Noisy/low-quality sources            | Score and decay source reliability dynamically             |
| False positive matches               | Use multi-factor scoring + manual QA loop                  |
| Overwhelming retail teams            | Filter by priority score + surface only reviewable SKUs    |
| Feedback fatigue                     | Use structured annotations + feedback-to-action visibility  |

---

## ✅ Outcome

A scalable, intelligent pipeline for tail acquisition—driven by data, refined by feedback, and built for scale.

> “Don’t just chase the long tail. Build the engine that absorbs it.”
