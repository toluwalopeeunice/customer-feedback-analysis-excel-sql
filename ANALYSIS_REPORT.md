
# Customer Feedback, Satisfaction & Service Resolution Analysis

**Tools:** Microsoft Excel and SQLite (SQL)  
**Reporting Period:** January 1, 2025 – August 14, 2026  
**Final Dataset:** 10,216 feedback records

---

## 1. Executive Summary

This project analyzed 10,216 customer feedback records to evaluate customer satisfaction, service resolution performance, and feedback patterns across categories, communication channels, and time.

Microsoft Excel was used to clean, standardize, validate, and document the dataset. SQLite was used to calculate key performance indicators (KPIs) and perform exploratory data analysis.

### Key Findings

- **Customer satisfaction:** Average rating of **3.92/5**, with **72.00%** of rated feedback receiving a rating of 4 or 5.
- **Service resolution:** **57.43%** of feedback records were marked as resolved.
- **Priority areas:** Pricing had the lowest average rating (**3.89/5**) and highest negative feedback rate (**14.32%**). Customer Service had the lowest resolution rate (**55.16%**).
- **Channel performance:** Survey had the highest average rating (**3.94/5**), while Live Chat had the highest resolution rate (**58.05%**).
- **Monthly trends:** Satisfaction remained relatively stable, without a clear sustained improvement or deterioration.

### Overall Conclusion

The findings indicate generally favorable ratings alongside opportunities to investigate service resolution processes.

Pricing and Customer Service are reasonable areas for further review, although differences between categories were modest.

Because the dataset contains missing values, conflicting identifiers, and potentially synthetic comments, the findings should be interpreted as a portfolio analysis rather than verified evidence of real-world customer behavior.

---

## 2. Business Problem and Objectives

### 2.1 Business Problem

Customer feedback provides information about satisfaction and service performance. However, inconsistent formatting, missing values, duplicate records, and incomplete resolution information can make it difficult to identify meaningful patterns.

This project examined customer ratings, feedback categories, communication channels, resolution statuses, and submission dates to identify potential areas for improvement.

### 2.2 Project Objectives

1. Clean and validate customer feedback data.
2. Measure overall customer satisfaction.
3. Evaluate service resolution performance.
4. Identify categories with relatively weaker satisfaction or resolution results.
5. Compare communication channels.
6. Examine monthly feedback volume and satisfaction trends.
7. Develop evidence-based recommendations.

### 2.3 Key Business Questions

- What is the overall satisfaction level?
- What percentage of feedback records are resolved?
- Which categories have the highest negative feedback rates?
- Which categories have the lowest resolution rates?
- How does performance vary across communication channels?
- How have feedback volume and satisfaction changed over time?
- How do ratings differ across resolution statuses?

### 2.4 Scope

The analysis covered 10,216 cleaned feedback records dated January 1, 2025, through August 14, 2026.

The project focused on descriptive analysis using Excel and SQLite. It did not attempt to establish causal relationships or infer sentiment from potentially unreliable comment text.

---

## 3. Dataset Overview

### 3.1 Dataset Description

The original dataset contained **10,331 feedback records** and nine fields.

After removing **115 exact duplicates**, the cleaned dataset contained **10,216 records**.

### 3.2 Original Dataset Fields

| Field | Description |
|---|---|
| FeedbackID | Feedback record identifier |
| CustomerName | Customer name |
| Email | Customer email address |
| Date | Feedback submission date |
| Rating | Customer rating from 1 to 5 |
| Category | Feedback category |
| Channel | Communication channel |
| ResolutionStatus | Case resolution status |
| Comment | Written feedback |

### 3.3 SQL Dataset Structure

Six fields were exported for SQL analysis:

| Field | Purpose |
|---|---|
| FeedbackID | Record identification and auditing |
| Category_Clean | Category comparisons |
| Channel_Clean | Channel comparisons |
| ResolutionStatus_Clean | Resolution analysis |
| Rating_Clean | Satisfaction calculations |
| Date_Clean | Time-based analysis |

The SQLite table was named `customer_feedback`.

Customer names and email addresses were excluded from the SQL export.

### 3.4 Data Quality Overview

| Issue | Records |
|---|---:|
| Exact duplicates removed | 115 |
| Missing ratings | 360 |
| Missing categories | 380 |
| Missing resolution statuses | 408 |
| Missing email addresses | 218 |

Seventeen repeated FeedbackID conflicts involving non-identical records were identified and retained for review.

Some comments also appeared generic or unrelated to the feedback context.

---

## 4. Tools and Methodology

### 4.1 Analytical Approach

The project followed a structured process of data inspection, cleaning, validation, SQL analysis, and interpretation.

**Microsoft Excel** was used for data preparation and documentation.

**SQLite**, accessed through DB Browser for SQLite, was used for querying and KPI calculations.

### 4.2 Excel Data Cleaning

The cleaning process included:

1. Removing exact duplicate records.
2. Standardizing text formatting.
3. Identifying missing values.
4. Standardizing and validating dates.
5. Checking feedback identifiers.
6. Reviewing comment completeness and relevance.
7. Reconciling record counts.
8. Documenting cleaning decisions.

The original worksheet was preserved, and a separate cleaning log recorded data-quality issues.

### 4.3 SQL Database Preparation

Six cleaned analytical fields were exported to CSV and imported into SQLite.

The initial SQL import contained 10,332 rows. Investigation identified **116 empty worksheet placeholders**, which were removed.

The final SQL table contained **10,216 records**, matching the cleaned Excel dataset.

Ratings were imported as text and converted to integers within SQL queries. Dates were also stored as text and transformed for chronological analysis.

### 4.4 SQL Techniques

The analysis used:

- `COUNT()` for feedback totals.
- `AVG()` for average ratings.
- `SUM()` and `CASE WHEN` for conditional calculations.
- `GROUP BY` for comparisons.
- `ORDER BY` for ranking and chronological ordering.
- `CAST()` for numeric conversion.
- `SUBSTR()` for date transformations.
- `COALESCE()` for missing-value labels.
- `NULLIF()` to avoid division by zero.

### 4.5 KPI Definitions

**Average Rating:** Mean of valid ratings on a five-point scale.

**Positive Feedback Rate:** Percentage of valid ratings equal to 4 or 5.

**Negative Feedback Rate:** Percentage of valid ratings equal to 1 or 2.

**Resolution Rate:** Percentage of all feedback records marked as resolved.

**Monthly Feedback Volume:** Number of feedback records in each calendar month.

Missing ratings were excluded from rating-based denominators. Missing resolution statuses remained in the denominator for resolution rates.

---

## 5. Data Cleaning and Quality Assessment

### 5.1 Duplicate Records

The original dataset contained 10,331 records.

A total of 115 exact duplicates were removed, leaving 10,216 records.

Seventeen repeated FeedbackID conflicts involving non-identical records were retained because matching identifiers alone did not prove the records were duplicates.

### 5.2 Missing Values

| Field | Missing Records | Percentage |
|---|---:|---:|
| Rating | 360 | 3.52% |
| Category | 380 | 3.72% |
| ResolutionStatus | 408 | 3.99% |
| Email | 218 | 2.13% |

Missing ratings were not replaced with artificial values.

Missing categories and resolution statuses were retained as identifiable unknown values.

### 5.3 Text and Date Standardization

Excel functions such as `TRIM`, `PROPER`, `LOWER`, and `SUBSTITUTE` were used to standardize text fields.

Dates were cleaned and validated in Excel. For SQL analysis, text dates stored in `DD/MM/YYYY` format were transformed into sortable year-month or ISO-style date strings.

Ambiguities in original date formats were documented as a limitation.

### 5.4 Rating Validation

The dataset contained **9,856 valid ratings** and **360 missing ratings**.

Valid ratings fell within the expected 1–5 scale.

SQL calculations converted valid rating strings into integers.

### 5.5 Customer Information and Comments

Customer names and email addresses were excluded from the analytical SQL export.

Comments were checked for completeness, but some appeared unrelated to genuine customer experiences. Sentiment analysis was therefore excluded.

### 5.6 SQL Import Validation

The initial SQL import contained 116 empty placeholder rows beyond the expected cleaned record count.

After verifying and deleting these placeholders, the SQL table contained exactly 10,216 records.

### 5.7 Quality Assessment Summary

The dataset was suitable for descriptive analysis after cleaning.

However, missing values, identifier conflicts, date-format ambiguity, and potentially synthetic comment content remained limitations.

---

## 6. SQL Analysis and Key Findings

### 6.1 Overall Customer Satisfaction

| KPI | Result |
|---|---:|
| Total feedback records | 10,216 |
| Records with valid ratings | 9,856 |
| Missing ratings | 360 |
| Average rating | 3.92/5 |
| Positive feedback records | 7,096 |
| Positive feedback rate | 72.00% |

**Insight:** Most rated feedback was favorable. The positive feedback rate describes rated records, not necessarily unique satisfied customers.

### 6.2 Satisfaction by Category

| Category | Average Rating | Negative Feedback Rate |
|---|---:|---:|
| Product Quality | 3.94 | 12.24% |
| Delivery Time | 3.94 | 12.61% |
| Website Experience | 3.91 | 12.96% |
| Returns Process | 3.91 | 13.11% |
| Customer Service | 3.90 | 14.03% |
| Pricing | 3.89 | 14.32% |

**Insight:** Pricing had the lowest average rating and highest negative feedback rate.

However, the difference between the highest and lowest category averages was only **0.05 points**.

The 380 records with missing categories were retained separately in the underlying analysis.

### 6.3 Overall Resolution Performance

| Resolution Status | Records | Percentage |
|---|---:|---:|
| Resolved | 5,867 | 57.43% |
| Pending | 1,998 | 19.56% |
| Escalated | 1,943 | 19.02% |
| Missing | 408 | 3.99% |
| **Total** | **10,216** | **100.00%** |

**Insight:** A total of 57.43% of records were marked resolved.

Pending and escalated records accounted for 38.58%, while 3.99% lacked a recorded resolution status.

The dataset did not include deadlines or resolution durations, so overdue cases could not be identified.

### 6.4 Resolution Rate by Category

| Category | Resolution Rate |
|---|---:|
| Customer Service | 55.16% |
| Pricing | 56.61% |
| Product Quality | 57.45% |
| Returns Process | 58.08% |
| Website Experience | 58.52% |
| Delivery Time | 58.57% |

**Insight:** Customer Service had the lowest resolution rate.

The difference between the highest and lowest category rates was **3.41 percentage points**.

Records with missing categories were retained in the overall analysis but omitted from this comparison table.

### 6.5 Satisfaction by Channel

| Channel | Average Rating |
|---|---:|
| Survey | 3.94 |
| Email | 3.93 |
| Phone | 3.91 |
| Live Chat | 3.91 |
| Social Media | 3.89 |

**Insight:** Survey had the highest average rating, while Social Media had the lowest.

The difference was only **0.05 points**.

### 6.6 Resolution Rate by Channel

| Channel | Resolution Rate |
|---|---:|
| Live Chat | 58.05% |
| Email | 57.68% |
| Survey | 57.65% |
| Social Media | 57.06% |
| Phone | 56.72% |

**Insight:** Live Chat had the highest resolution rate and Phone the lowest, with a difference of **1.33 percentage points**.

### 6.7 Monthly Feedback Volume

The dataset covered 20 calendar months.

- **Highest complete month:** August 2025, with 576 records.
- **Lowest complete month:** February 2026, with 433 records.
- **August 2026:** 194 records, representing a partial month ending August 14.

**Insight:** Monthly volume fluctuated without a clear sustained upward or downward trend.

The partial final month should not be interpreted as evidence of declining engagement.

### 6.8 Monthly Satisfaction Trends

- **Highest average rating:** March 2026 — 4.01/5.
- **Lowest average rating:** February 2025 — 3.83/5.
- **Highest positive feedback rate:** July 2025 — 74.76%.
- **Lowest positive feedback rate:** February 2025 — 69.13%.

**Insight:** Monthly satisfaction remained relatively stable, with no clear sustained improvement or deterioration.

### 6.9 Satisfaction by Resolution Status

| Status | Average Rating | Positive Feedback Rate |
|---|---:|---:|
| Escalated | 3.95 | 72.10% |
| Missing | 3.92 | 72.63% |
| Resolved | 3.91 | 71.91% |
| Pending | 3.90 | 72.03% |

**Insight:** Satisfaction measures differed only slightly across resolution statuses.

The timing of ratings relative to case resolution was unavailable, so the analysis could not determine whether resolution outcomes influenced satisfaction.

### 6.10 Summary of Findings

The analysis identified five major findings:

1. Customer ratings were generally favorable.
2. Resolution performance warranted further investigation.
3. Pricing and Customer Service were potential review priorities.
4. Channel performance differences were modest.
5. Monthly satisfaction was relatively stable.

---

## 7. Business Recommendations

### 7.1 Investigate Pricing-Related Feedback

**Finding:** Pricing had the lowest average rating (3.89/5) and highest negative feedback rate (14.32%).

**Recommendation:** Review verified pricing complaints and supporting information to identify possible concerns about transparency, value, discounts, or unexpected charges.

**Expected Benefit:** More specific evidence could guide targeted improvements to pricing communication.

### 7.2 Review Customer Service Workflows

**Finding:** Customer Service had the lowest resolution rate (55.16%) and a relatively high negative feedback rate (14.03%).

**Recommendation:** Review case assignment, ownership, escalation procedures, and closure practices.

**Expected Benefit:** Potential process inefficiencies could be identified and addressed.

### 7.3 Strengthen Resolution Tracking

**Finding:** Only 57.43% of records were marked resolved; 38.58% were pending or escalated, and 3.99% had missing statuses.

**Recommendation:**

1. Standardize resolution status definitions.
2. Keep case statuses updated.
3. Assign ownership for pending and escalated cases.
4. Record creation, escalation, and closure dates.
5. Introduce appropriate service-level targets.

**Expected Benefit:** Better visibility into case progress and future analysis of resolution times.

### 7.4 Monitor Communication Channels

**Finding:** Satisfaction and resolution differences across channels were relatively small.

**Recommendation:** Continue monitoring channel performance while collecting information about case complexity, staffing, and response times.

**Expected Benefit:** Better evidence for determining whether channel-specific improvements are necessary.

### 7.5 Improve Data Quality

**Finding:** Missing values and conflicting feedback identifiers affected data completeness and reliability.

**Recommendation:** Strengthen validation rules, standardize dates and categorical values, investigate identifier conflicts, and conduct regular data-quality audits.

**Expected Benefit:** More reliable KPIs and efficient future analysis.

### 7.6 Establish Recurring Reporting

**Finding:** Satisfaction remained relatively stable throughout the reporting period.

**Recommendation:** Produce regular reports covering satisfaction, negative feedback, resolution status, channel performance, monthly trends, and data completeness.

**Expected Benefit:** Earlier identification of emerging patterns and clearer evaluation of operational changes.

### 7.7 Recommended Priorities

| Priority | Action |
|---|---|
| High | Review resolution tracking and follow-up |
| High | Investigate Customer Service workflows |
| Medium | Investigate pricing-related feedback |
| Medium | Improve data validation and completeness |
| Ongoing | Monitor satisfaction across channels and months |

These priorities are provisional and should be refined using operational context and additional evidence.

---

## 8. Limitations and Future Improvements

### 8.1 Missing and Inconsistent Data

The dataset contained missing ratings, categories, resolution statuses, and email addresses.

Seventeen repeated FeedbackID conflicts involving non-identical records remained unresolved.

**Future Improvement:** Strengthen data validation and investigate identifier conflicts.

### 8.2 Limited Resolution Information

The dataset did not contain case creation, escalation, or closure timestamps.

Resolution times, overdue cases, and service-level performance could not be measured.

**Future Improvement:** Collect timestamps and relevant service-level targets.

### 8.3 No Causal Evidence

Observed differences between categories, channels, and statuses were descriptive.

The analysis could not establish what caused changes in satisfaction.

**Future Improvement:** Collect additional operational variables and apply appropriate statistical or experimental methods.

### 8.4 Potentially Unreliable Comments

Some comments appeared generic or unrelated to feedback.

**Future Improvement:** Use verified, authentic comments before conducting sentiment analysis.

### 8.5 Unverified Dataset Representativeness

The dataset's real-world authenticity and representativeness could not be independently confirmed.

**Future Improvement:** Use documented, verified operational data where available.

### 8.6 Partial Reporting Period

August 2026 contained only data through August 14.

**Future Improvement:** Compare complete months and clearly label partial periods.

### 8.7 Analytical Scope

The project focused on descriptive Excel and SQL analysis. It did not include predictive modeling, statistical significance testing, or an interactive dashboard.

**Future Improvement:** Expand analysis when additional data and business requirements justify it.

---

## 9. Conclusion

This project demonstrated an end-to-end data analysis workflow using Microsoft Excel and SQLite.

Starting with 10,331 original feedback records, the cleaning process removed 115 exact duplicates and produced a final dataset of 10,216 records.

Excel was used for data cleaning, validation, and documentation, while SQL was used to calculate KPIs, compare categories and channels, and examine monthly trends.

### Key Conclusions

1. **Customer satisfaction was generally favorable**, with an average rating of 3.92/5 and a positive feedback rate of 72.00%.
2. **Resolution performance warranted review**, with 57.43% of records marked resolved.
3. **Pricing and Customer Service were potential investigation priorities**, based on comparatively weaker satisfaction or resolution indicators.
4. **Communication channel differences were modest**, suggesting the need for more evidence before making major changes.
5. **Monthly satisfaction was relatively stable**, without a clear sustained improvement or deterioration.

### Skills Demonstrated

- Excel data cleaning and validation
- Duplicate detection and missing-value assessment
- SQL aggregation and conditional calculations
- Data type and date transformations
- KPI development
- Exploratory data analysis
- Business recommendations
- Professional analytical reporting

### Final Statement

Overall, the project demonstrates the ability to transform imperfect raw data into a cleaned analytical dataset, use SQL to generate structured insights, and communicate findings in a professional business report.

Because the dataset's authenticity and representativeness could not be verified, the findings should be interpreted as a portfolio demonstration rather than confirmed evidence about a real-world business.

---

**Project:** Customer Feedback, Satisfaction & Service Resolution Analysis  
**Tools:** Microsoft Excel | SQLite | SQL  
**Purpose:** Data Analyst Portfolio
