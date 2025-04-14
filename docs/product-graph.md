# 🕸️ Product Graph in Catalog Systems

A Product Graph is the structural backbone of a smart catalog. It enables discovery, enrichment, and inference by linking items through meaningful relationships. Unlike flat catalogs, a product graph treats items as interconnected entities, making it a foundation for scalable relevance, recommendations, and decision support.

---

## 1. 🧱 Core Components of the Product Graph

### Nodes
Each node represents a unique product or product variant.
- SKU-level: individual seller listings
- Product-level: normalized product entity (merged across listings)
- Meta-entity: attribute clusters like brand, subcategory

### Edges
Edges represent relationships between nodes:

| Edge Type           | Example                                                  | Use Case                          |
|---------------------|-----------------------------------------------------------|-----------------------------------|
| Variant             | iPhone 14 128GB ↔ iPhone 14 256GB                         | Navigation between options        |
| Substitute          | Samsung Galaxy Tab S8 ↔ Apple iPad Air                    | Reco alternatives                 |
| Bundle              | Toothbrush ↔ Toothpaste                                   | Complementary suggestions         |
| Brand Group         | Nike Running Shoes ↔ Nike Yoga Pants                      | Brand storefront, filters         |
| Shared Attributes   | Almond Milk 1L ↔ Almond Milk 500ml                        | Tag-based clustering              |
| Session Link        | Products viewed together in session                       | Session-based recommendations     |

---

## 2. 🛠️ Graph Construction Pipeline

### a. Entity Resolution
- Deduplicate listings to form unified product nodes
- Normalize brand, model, size, and format

### b. Attribute-Based Linking
- Compute pairwise similarity across structured fields (brand, category, size)
- Use learned thresholds to add edges (e.g., >0.85 similarity score)

### c. Behavioral Linking
- Construct edges using co-view, co-cart, co-purchase signals
- Apply decay weights based on frequency and recency

### d. Predictive Modeling for Edge Scoring
To determine if two products should be linked as substitutes or complements, we:
- Train **XGBoost** and other tree-based models
- Use features like:
  - Brand match
  - Price delta
  - Co-view sessions
  - Clickstream similarity
  - Conversion funnel depth
- Output is a scored edge: high-confidence substitute, potential bundle, or exclude

### ✅ Example
- Products: `Colgate Total Advanced 120g` and `Sensodyne Repair & Protect 100g`
- Edge: Substitute (category = toothpaste, brand ≠ same, high match score from XGBoost)

---

## 3. 📊 Graph Features for ML Models

The product graph can power and enhance various ML systems:

| Use Case              | Graph Feature Inputs                          |
|------------------------|-----------------------------------------------|
| Similarity scoring     | Shortest path, common attributes, co-view     |
| Recommendation model   | Degree centrality, weighted neighbors         |
| Search re-ranking      | Path strength to top result, graph cluster ID |
| Cold start products    | Graph-based embeddings                        |

### ✅ Embedding Example
Use node2vec / GraphSAGE to learn embeddings:
```python
similarity = cosine(embedding[p1], embedding[p2])
```
Train recos on graph neighborhood representations to improve relevance.

---

## 4. 🔄 Graph Updates & Maintenance

- **Streaming Updates**: Session-based edges, new listings
- **Batch Updates**: Attribute inference, brand normalization
- **Edge Aging**: Decay infrequently traversed behavioral edges
- **Versioning**: Keep snapshot of graphs used in experiments

### ✅ Change Management
- Every graph update → versioned + scored for:
  - Coverage (% of catalog linked)
  - Precision (manual QA samples)
  - RecSys delta (win ratio before/after)

---

## 5. 🧠 Product Graph Health Metrics

| Metric                      | Insight Provided                                  |
|-----------------------------|---------------------------------------------------|
| Node Coverage %             | How many products are linked into the graph      |
| Avg. Degree per Node        | Graph richness; too sparse = poor connectivity    |
| % High-Confidence Edges     | Signal quality across graph                      |
| Navigation Success Rate     | Drop-off after user clicks graph-based reco      |

---

## ⚠️ Risks & Mitigations

| Risk                        | Mitigation                                       |
|-----------------------------|--------------------------------------------------|
| Overlinked Products         | Tune similarity threshold, apply diversity caps  |
| Stale Behavioral Edges      | Use decay + last-timestamp edge filtering        |
| Edge Explosion              | Use degree-limited pruning per node              |
| Noise from Aggressive Inference | Validate with retail QA + metadata fallback |

---

## ✅ Outcome

A dynamic graph layer that:
- Connects catalog entities semantically and behaviorally
- Powers intelligent recommendations and search
- Learns from user data and improves over time
- Integrates predictive models like XGBoost for substitute edge scoring

> “Flat catalogs show what’s there. Product graphs reveal what’s connected.”
