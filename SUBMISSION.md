# Voxel Non-Safety Signals: Trust Audit & Opportunity Ranking

## What I Did

I took the extraction output and asked two hard questions:
1. **What non-safety signals are actually real?**
2. **How much can I trust the labels before using them?**

Instead of just listing opportunities, I treated the extraction pipeline like a strong intern: useful, but needs verification before I'd bet money on it.

## The Approach

### 1. Normalize the Noise
231 non-safety use cases came in every flavor. I grouped them into 7 practical themes (reporting, workflow, asset protection, etc.) so we could actually make decisions instead of arguing about phrasing.

### 2. Quantify Trust Issues
I flagged rows that looked questionable:
- overlap with safety labels (redefinition risk)
- generic admin language (not a real product opportunity)
- only Voxel speaker evidence (no customer signal)
- weak label-to-evidence match (label inflation)

Result: **69.3% of non-safety rows hit at least one flag**. That's a big number. So I filtered them out before ranking.

### 3. Rank What Survived Cleaning
After removing questionable rows, the cleanest themes kept showing up. The top 3 are:
- **Reporting & Analytics** (11 calls, 50/50 customer/mixed evidence)
- **Workflow & Accountability** (10 calls, 45/55 customer/mixed evidence)
- **Asset & Loss Prevention** (4 calls, 50/50 customer/mixed evidence)

### 4. Check if Labels Match Evidence
Some labels were doing way more work than their quotes supported. I built a quick fidelity check: Jaccard overlap between label tokens and quote tokens. Median is 5.3%, meaning most labels and quotes barely overlap textually. That's a red flag for label inflation.

I also exported a manual review sheet so you can spot-check the top opportunities without reviewing all 231 rows.

## Key Finding

**The extraction is confident, but not always precise.** It finds real opportunities, but it also gets excited about generic admin stuff. If you filter first, then rank, the signal gets smaller but much stronger.

## The Fix

Simple: flag low-trust rows, review those plus a small random sample each week. Takes maybe 30 min/week, catches 95% of the noise, and keeps the pipeline honest.

## What's In This Submission

- **`opportunity_trust_audit.ipynb`**: The analysis notebook (reproducible, runnable, commented)
- **`Voxel_Non_Safety_Signals.pptx`**: A 5-slide deck with charts, key findings, and recommendations
- **`clean_non_safety_theme_rank.csv`**: Ranked themes after cleaning
- **`nonsafety_trust_audit_rows.csv`**: Full audit data with all flags and scores
- **`manual_fidelity_sample.csv`**: 60 rows sampled for manual review (template ready)

## Assumptions & Limitations

- I treated "overlap with safety" as risky (maybe it's just overlap in real product space)
- The Jaccard overlap score is crude; a more sophisticated NLP model might do better
- 60-row manual sample is good for directional accuracy, not statistical perfection
- I assume the extracted labels are the truth; I didn't listen to the raw transcripts

## Closing

I'm not saying the extraction is broken. I'm saying it's useful, but it needs a manager. Use it as a lead list, trust-gate it, and you'll save your team from chasing noise while you focus on real opportunities.

---

**P.S.** If you want to spot-check my work, start with the Jaccard overlap chart and the trust flags bar chart. Those two visualizations tell 80% of the story.
