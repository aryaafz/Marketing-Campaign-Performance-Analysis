# 📣 Marketing Campaign Performance Analysis & Interactive Power BI Dashboard

## 📌 Project Overview

This project analyzes 10,000 marketing campaigns run across 5 channels (Search, Display, Social, Email, Influencer) to evaluate revenue, profitability, efficiency, and customer acquisition performance — and, critically, to test whether the differences observed between channels are **statistically significant** before turning them into budget recommendations.

The project follows a complete data analytics workflow: **data cleaning with logical/funnel validation**, **feature engineering**, **exploratory & bivariate analysis** answering 13 specific business questions, **statistical significance testing (Levene's Test + one-way ANOVA)**, and an **interactive Power BI dashboard** — ending with recommendations that are explicit about their level of statistical confidence.

---

## 🎯 Business Problem

The company invests in multiple marketing channels but lacks a rigorous, statistically validated answer to:

1. Which channel actually generates the highest revenue, profit, and efficiency (ROI/ROAS) — and are these differences real, or within normal variation?
2. Which channel acquires customers most cost-effectively?
3. Does spending more, or running campaigns longer, reliably improve returns?
4. Do funnel-stage metrics (CTR, Conversion Rate) meaningfully differ by channel?

Marketing budget decisions risk being driven by small, visually appealing differences between channels that may not hold up under statistical scrutiny.

---

## 🎯 Project Objectives

- Clean and validate 10,000 campaign records, including funnel-logic checks (Clicks ≤ Impressions ≤ Leads ≤ Conversions) and recalculated-metric validation.
- Answer 13 specific business questions through bivariate analysis and correlation testing.
- Test whether observed channel-level differences in Revenue, ROI, and CPA are statistically significant using one-way ANOVA.
- Translate findings into recommendations that are explicit about confidence level, avoiding overstated claims.
- Build an interactive Power BI dashboard that communicates both the performance patterns and their statistical uncertainty.

---

# 🗂 Dataset

- **Dataset:** Marketing Campaign Performance
- **Records:** 10,000 campaigns
- **Channels:** Search, Display, Social, Email, Influencer

Main features include: CampaignID, StartDate, EndDate, Channel, Impressions, Clicks, Leads, Conversions, Cost_USD, Revenue_USD, ROI.

---

# 🧹 Data Cleaning

- ✅ Checked duplicate records — none found.
- ✅ Converted StartDate/EndDate to datetime format.
- ✅ Validated funnel logic (Clicks ≤ Impressions, Leads ≤ Clicks, Conversions ≤ Leads) — 0 invalid records found.
- ✅ Recalculated ROI independently from `(Revenue − Cost) / Cost × 100` and validated it against the dataset's existing ROI column — results matched exactly (0.00 difference), confirming data integrity.
- ✅ No missing values across any of the 11 original columns (confirmed via df.info()).

---

# ⚙ Feature Engineering

- Campaign_Duration (days between StartDate and EndDate)
- CTR (Clicks / Impressions), CPC (Cost / Clicks)
- Conversion_Rate (Conversions / Leads), CPA (Cost / Conversions)
- Profit (Revenue − Cost), ROAS (Revenue / Cost)

---

# 📊 Exploratory Data Analysis — 13 Business Questions Answered

### Channel Performance
1. Which channel generates the highest average revenue? → **Display** ($5,178.89)
2. Which channel produces the highest ROI? → **Search** (101.33%)
3. Which channel generates the highest profit? → **Display** ($2,596.39)
4. Which channel achieves the highest CTR? → Nearly uniform across all channels (5.43%–5.52%)
5. Which channel converts leads most effectively? → Nearly uniform across all channels (40.09%–40.28%)
6. Which channel has the lowest CPA? → **Influencer** ($9.11)
7. Which channel has the highest ROAS? → **Search** (2.01)

### Spending & Duration Effects
8. Does higher spending lead to higher revenue? → Yes, strongly (r = 0.86, p < 0.001)
9. Does higher spending always produce higher ROI? → No relationship found (r = -0.007, p = 0.472)
10. Does campaign duration affect performance? → No relationship found (r = 0.015, p = 0.125)

### Funnel Relationships
11. Do more leads result in more conversions? → Yes, strong positive relationship
12. Do more clicks generate more leads? → Yes, strong positive relationship
13. Which KPIs correlate most strongly with revenue and ROI? → Cost is the strongest driver of Revenue; no KPI meaningfully predicts ROI

---

# 📐 Statistical Significance Testing

Channel-level differences in Revenue, ROI, and CPA were tested using **one-way ANOVA** (after confirming homogeneous variance via Levene's Test, p > 0.05 for all three metrics):

| Metric | F-statistic | p-value | Significant? |
|---|---|---|---|
| Revenue_USD | 1.168 | 0.323 | No |
| ROI | 0.612 | 0.654 | No |
| CPA | 1.043 | 0.383 | No |

**None of the observed channel-level differences are statistically significant at the 95% confidence level.** Patterns such as Display's higher revenue or Search's higher ROI are directional signals worth monitoring, not confirmed effects — and are treated that way throughout this project's recommendations.

---

# 💡 Key Findings

1. **Display leads in absolute revenue and profit, while Search leads in efficiency — but neither difference is statistically significant** (ANOVA p > 0.05 for Revenue, ROI, CPA).
2. **Influencer shows the lowest CPA**, a promising but statistically unconfirmed cost advantage.
3. **CTR and Conversion Rate do not meaningfully differ by channel** — channel choice does not appear to influence funnel-stage behavior.
4. **Campaign spending drives revenue but not efficiency or duration** — more budget or more days does not reliably improve ROI.
5. **Funnel stages reinforce each other** — improvements in clicks consistently carry through to leads and conversions.

---

# 📈 Strategic Recommendations

1. **Treat channel-level differences as directional signals, not confirmed effects.** Avoid large, irreversible budget reallocations based on current averages alone; validate with small-scale A/B budget testing.
2. **Use Search's efficiency profile as a benchmark** for targeting and creative optimization across other channels.
3. **Test Influencer campaign expansion at a controlled scale** rather than committing a large budget shift upfront.
4. **Do not use CTR, Conversion Rate, or campaign duration as budget-allocation levers** — they show no meaningful variation or correlation with financial outcomes.
5. **Adopt a multi-KPI, statistically-grounded evaluation framework** — pair channel comparisons with significance testing before treating any channel as a confirmed top or bottom performer.

---

# 📊 Power BI Dashboard

The interactive dashboard consists of **two pages**, deliberately designed with neutral, single-color charts (rather than red/green highlighting) to avoid visually overstating differences that were not statistically confirmed.

## 1️⃣ Channel Performance Overview
- KPI cards: Total Revenue, Total Profit, Average ROI, Average ROAS, Campaign Count
- Average Revenue, Profit, ROI, and ROAS by Channel (bar charts, Y-axis starting at 0 to avoid visual distortion)
- Note callout: *"Channel-level differences shown here are directional. ANOVA testing found no statistically significant difference between channels (p > 0.05 for Revenue, ROI, and CPA)."*
- Slicers: Channel, Start_Month

## 2️⃣ Funnel & Channel Efficiency
- Marketing Funnel: Impressions → Clicks → Leads → Conversions
- Average CTR and Conversion Rate by Channel
- Cost vs. ROI scatter plot (all 10,000 campaigns, unaggregated) — visually confirms the absence of correlation
- Average CPA by Channel

---

# 🛠 Tools & Technologies

- Python (Pandas, NumPy, SciPy, Matplotlib, Seaborn)
- Jupyter Notebook
- Power BI

---

# 🚀 Project Highlights

✔ End-to-end data analytics workflow, from raw data to statistically-validated business recommendation
✔ Funnel-logic and recalculated-metric validation during data cleaning
✔ 13 business questions systematically answered through bivariate analysis
✔ Formal statistical significance testing (Levene's Test + one-way ANOVA) applied before drawing conclusions
✔ Recommendations explicitly calibrated to their statistical confidence level, avoiding overstated claims
✔ Dashboard design choices (neutral colors, zero-based axes) intentionally aligned with the statistical findings
