Below is a **15-minute demo outline** focusing on **why** you introduced feature selection (to ensure potential consumers remain in-cluster) and **how** you generate insights (showing tables in Hue). This outline **avoids** technical details about Spark, emphasizing the **business logic** and **tables** instead.

---

## 1. Introduction (1–2 minutes)

- **Context**:  
  1. We originally had **56 features** when clustering PWM and consumers.  
  2. We only consider **consumers** to be in a cluster if they’re “within range,” meaning **no farther** from the cluster center than the **farthest** existing PWM in that cluster.  
  3. **Problem**: Some features **overly differentiate** PWM vs. consumer, pushing potential PWM converters **out** of the cluster. As a result, these consumers were **never captured** even though they converted within six months.  

- **Solution**:  
  - We perform **feature selection** to use a smaller, more balanced subset of features. That way, the “cluster range” is not too narrow—ensuring the **majority** of potential converting consumers fall **within** the cluster.

**Talking Point**: “We realized we needed fewer, more relevant features so that clusters would capture upcoming PWM converters, rather than excluding them due to strict distances in high-dimensional space.”

---

## 2. Feature Selection (4–5 minutes)

- **What & Why**  
  1. We train a **random forest** classifier to distinguish consumers who actually become PWM vs. those who don’t (or existing PWM vs. consumer data).  
  2. **Rank** the features by their contribution to that classification.  
  3. **Pick the top** subset (e.g., top 20) that best separates PWM from consumer **without** overly shrinking cluster distance ranges.

- **Show in Hue**  
  1. **Features Table** (the original table with 56+ columns).  
  2. **Selected Features Table** – highlight how it only has, for example, 20 top-ranked feature names.  
  3. Emphasize that this smaller feature set is what we use in clustering so potential PWM consumers remain within the cluster distance threshold.

**Demo Actions**:
- In Hue, open the **features table**: briefly mention columns.  
- Switch to the **selected_features** table: highlight the fewer columns.  
- Briefly mention how the selection logic ensures a broader cluster “range.”

---

## 3. Updated Clustering & PWM Assignments (3–4 minutes)

- **Clustering with Fewer Features**  
  - We run the same K-Means logic, but only on the selected columns.  
  - The **range** for each cluster (farthest PWM distance) is now **less restrictive** on unimportant dimensions, so more **potential** PWM consumers are included in the correct cluster.

- **PWM Table with `cluster_id`**  
  1. Show the **PWM table** in Hue: each existing PWM client with a final `cluster_id` assigned.  
  2. This table is minimal, containing just the essential info plus `cluster_id`.

**Demo Actions**:
- In Hue, open the **PWM table**. Show a few rows with `cluster_id`.  
- Mention that only the top features matter for these distances.

---

## 4. Prospect Insights (4–5 minutes)

- **Why**: Business teams want to know **why** a prospect belongs to a cluster—what makes them similar to existing PWM?

- **Process**:  
  1. For each cluster, we do a small “cluster vs. rest” model to identify which features stand out.  
  2. Compute **mean ± 2*std** for those features among **existing PWM** in that cluster.  
  3. For each **prospect** in that cluster, we record how each top feature’s value compares to the cluster’s typical range.  
  4. The result is a **long “insight” string** summarizing these differences.

- **Prospects Table with `insight`**  
  1. Show the final table in Hue: `[hh_id_in_wh, similarity_score, distance_to_center, prospect_segment, cluster_id, insight, business_date]`.  
  2. Point out the **`insight`** column, which might say:  
     > `"bal_amt_sum is 10,000; cluster mean=12,000; range=[8,000–16,000]"`  
     or similar lines for the top 5 features.

**Demo Actions**:
- In Hue, open the **prospects table** with the `insight` column.  
- Scroll through a couple of example rows, highlight how the text references the top features, the prospect’s value, and the cluster’s typical range.

---

## 5. Wrap-Up & Q&A (1–2 minutes)

- **Key Takeaways**:  
  - We **reduced** from 56 to a manageable subset of features so cluster distance thresholds wouldn’t exclude potential PWM consumers.  
  - We’re now able to **explain** each prospect’s placement via a **multi-feature insight** string.  
  - All this data is **visible** in Hue: the features table, the selected features table, the PWM table, and the final prospect table with insights.

- **Questions?**  

---

### Timing Recap

1. **Intro (Feature-Selection Motivation)** – 1–2 minutes  
2. **Feature Selection** – 4–5 minutes  
3. **Clustering & PWM Table** – 3–4 minutes  
4. **Prospects & Insight Generation** – 4–5 minutes  
5. **Conclusion/Q&A** – 1–2 minutes  

**Total**: ~15 minutes.  

This structure should keep the focus on **why** fewer features help capture potential PWM consumers, **how** the final pipeline works, and **what** data tables your team can see in Hue.
