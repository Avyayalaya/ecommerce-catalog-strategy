# 🛒 Winning on Catalog: Strategy to Scale E-commerce Selection

Selection remains fundamental to winning in any e-commerce market—alongside pricing and delivery. It is ultimately about two goals:

1. **Having everything the customer wants**
2. **Knowing and surfacing what the customer wants**

---

## 🔗 Key Problems in the Selection Value Chain

### 1. 📈 Catalog Expansion – Scaling the Tail Programmatically

Traditional vendor/category team models cannot scale tail selection due to linear cost curves. A programmatic approach is essential.

#### a. Identification & Extraction
- Start with **Top 50 sources** (online + offline)
- Scale **only** after achieving stability in the ingestion-processing-feedback loop

#### b. Processing Engine
- Store in a **flattened dataset** of external catalog items
- Construct a **Product Graph**
- Use a **Matching Algorithm** to detect true gaps vs. existing catalog

#### c. Metadata Enrichment
- Use signals like **brand**, **adjacent revenue pools**, and **similar products**
- Layer ML-based recommendations to infer importance and trends

#### d. Channel to Retail
- Build **internal tools** for Retail, SLT to:
  - Monitor progress
  - Provide high-signal feedback

#### e. Feedback Loops
- Feedback from humans-in-the-loop → re-train models + enrich metadata
- Improves matching and filtering logic over time

#### f. Team Composition
- Beyond ML/DS teams:
  - Build a pool of **Technical PMs**
  - Skillset: ML understanding, Big Data, Data Engineering, Platform Architecture
  - Also capable of doing ‘Technical Sales’ for internal stakeholder adoption

---

### 2. 🧠 Catalog Excellence – Search + Recommendation Flywheel

Winning here requires tackling a **weak-link** (search failure) and **strong-link** (delightful recommendation) problem.

#### a. Weak-Link: Eliminate Failed Searches

> “No results found” or irrelevant outputs on specific, high-intent queries (e.g. `Nike`) are unacceptable.

##### 📌 Solution:

1. **Systematic Failed Search Program**
   - Merge query logs with external catalog datasets
   - Build a failure taxonomy across categories

2. **Query Replication Strategy**
   - Pull top 5000 queries/category
   - Identify failed ones
   - Auto-scrape result set and:
     - Match with internal catalog
     - If not present → match with external sources
     - Prioritize acquisition or internal indexing

3. **Search Team Feedback Loop**
   - Flag items on catalog but missing in search results
   - Create a reverse-feedback loop for indexing and ranking improvement

---

#### b. Strong-Link: Surfacing World-Class Recommendations

> Recommendations are split into:
> - **Alternatives**: Needed in Search Result Pages
> - **Complementary**: Needed on Product Pages

##### 📌 Core Strategy:

1. **Similarity Score Model**
   - Features: brand, glance views, price, units sold, availability
   - Dynamically updated from live session data

2. **Graph-Integrated Learning**
   - Real-time updates to product graph
   - ML model trained on “win ratio” of clicked recos → conversion

---

## 📊 Summary of Systems

| Area               | Focus                          | Key Enablers                                   |
|--------------------|-------------------------------|------------------------------------------------|
| Catalog Expansion  | Tail selection                | Web scraping, Product Graph, Matching, Feedback |
| Metadata Enrichment| Value from adjacent items     | ML Models, Similarity Scoring                   |
| Failed Search      | Zero tolerance for failure    | Query Logs, Automated Sourcing, Search Feedback|
| Recommendations    | Delight through alternatives  | Real-time Data, Product Graph, Win-Ratio ML     |
| Team               | Scale + Adoption              | Technical PMs, DS, Big Data Engineers           |

---

## 📎 Things to Do

- [ ] Define top 50 catalog sources by category
- [ ] Build ingestion → flattening → matching pipeline
- [ ] Setup feedback annotation interfaces for internal teams
- [ ] Train similarity scoring model using live user signals
- [ ] Integrate feedback from failed search into search relevance engine
