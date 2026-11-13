
# Customer Feedback, Satisfaction & Service Resolution Analysis

## Project Overview

This project analyzes 10,216 customer feedback records using Microsoft Excel and SQLite to evaluate customer satisfaction, service resolution performance, and feedback trends.

The analysis covers January 1, 2025, to August 14, 2026.

## Tools Used

- Microsoft Excel — data cleaning, validation, and documentation
- SQLite (DB Browser for SQLite) — SQL analysis and KPI calculations
- GitHub — project documentation and portfolio presentation

## Business Objectives

- Measure overall customer satisfaction.
- Evaluate feedback resolution performance.
- Identify categories with relatively lower satisfaction.
- Compare performance across communication channels.
- Analyze monthly feedback volume and satisfaction trends.
- Recommend potential areas for improvement.

## Data Cleaning

The original dataset contained 10,331 records.

Cleaning activities included:

- Removing 115 exact duplicate records.
- Standardizing text and date formats.
- Identifying and documenting missing values.
- Flagging conflicting feedback identifiers.
- Validating the final dataset before SQL analysis.

The final analytical dataset contained 10,216 records.

## Key Findings

| Metric | Result |
|---|---|
| Total feedback records | 10,216 |
| Average customer rating | 3.92/5 |
| Positive feedback rate | 72.00% |
| Overall resolution rate | 57.43% |
| Lowest-rated category | Pricing (3.89/5) |
| Lowest category resolution rate | Customer Service (55.16%) |
| Highest-rated channel | Survey (3.94/5) |
| Highest channel resolution rate | Live Chat (58.05%) |

Positive feedback was defined as a rating of 4 or 5, calculated as a percentage of records with valid ratings.

## Business Recommendations

1. Investigate pricing-related customer concerns.
2. Review Customer Service resolution workflows.
3. Strengthen tracking of pending and escalated cases.
4. Improve data completeness and validation.
5. Monitor customer satisfaction and resolution metrics regularly.

## Project Files

- `customer_feedback_analysis.sql` — SQL queries used for the analysis.
- Excel cleaning workbook — prepared locally; public release subject to privacy review.
- Final analysis report — prepared separately.

## Limitations

The dataset contains missing values, conflicting feedback identifiers, and potentially synthetic comment text.

The analysis is descriptive and does not establish causal relationships or verified real-world customer behavior.

## Skills Demonstrated

Data Cleaning | Microsoft Excel | SQL | SQLite | Data Validation | KPI Analysis | Business Reporting
