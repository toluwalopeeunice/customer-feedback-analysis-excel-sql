
-- Project: Customer Feedback, Satisfaction & Service Resolution Analysis
-- Tools: Microsoft Excel and SQLite
-- Purpose: Analyze customer feedback and service resolution performance

-- 1. Total feedback records
SELECT COUNT(*) AS total_feedback
FROM customer_feedback;


-- 2. Overall customer satisfaction
SELECT
    COUNT(*) AS total_feedback,
    COUNT(
        CASE
            WHEN Rating_Clean IN ('1', '2', '3', '4', '5')
            THEN 1
        END
    ) AS rated_feedback,
    ROUND(
        AVG(
            CASE
                WHEN Rating_Clean IN ('1', '2', '3', '4', '5')
                THEN CAST(Rating_Clean AS INTEGER)
            END
        ), 2
    ) AS average_rating
FROM customer_feedback;


-- ============================================================
-- CUSTOMER FEEDBACK, SATISFACTION & SERVICE RESOLUTION ANALYSIS
-- SQL PORTFOLIO PROJECT
-- Database: SQLite
-- Table: customer_feedback
-- ============================================================

-- 3. Rating distribution
SELECT
    COALESCE(Rating_Clean, 'Missing') AS rating,
    COUNT(*) AS feedback_count
FROM customer_feedback
GROUP BY Rating_Clean
ORDER BY Rating_Clean;


-- 4. Overall positive feedback rate
-- Positive ratings = 4 or 5
-- Denominator = records with valid ratings
SELECT
    COUNT(CASE
        WHEN Rating_Clean IN ('4', '5') THEN 1
    END) AS positive_feedback,
    COUNT(CASE
        WHEN Rating_Clean IN ('1', '2', '3', '4', '5') THEN 1
    END) AS rated_feedback,
    ROUND(
        100.0 * COUNT(CASE
            WHEN Rating_Clean IN ('4', '5') THEN 1
        END)
        / NULLIF(COUNT(CASE
            WHEN Rating_Clean IN ('1', '2', '3', '4', '5') THEN 1
        END), 0),
        2
    ) AS positive_feedback_rate
FROM customer_feedback;


-- 5. Satisfaction by feedback category
SELECT
    COALESCE(Category_Clean, 'Missing') AS category,
    COUNT(*) AS total_feedback,
    COUNT(CASE
        WHEN Rating_Clean IN ('1', '2', '3', '4', '5') THEN 1
    END) AS rated_feedback,
    ROUND(AVG(CASE
        WHEN Rating_Clean IN ('1', '2', '3', '4', '5')
        THEN CAST(Rating_Clean AS INTEGER)
    END), 2) AS average_rating
FROM customer_feedback
GROUP BY COALESCE(Category_Clean, 'Missing')
ORDER BY average_rating DESC;


-- 6. Negative feedback rate by category
-- Negative ratings = 1 or 2
SELECT
    COALESCE(Category_Clean, 'Missing') AS category,
    COUNT(CASE
        WHEN Rating_Clean IN ('1', '2') THEN 1
    END) AS negative_feedback,
    COUNT(CASE
        WHEN Rating_Clean IN ('1', '2', '3', '4', '5') THEN 1
    END) AS rated_feedback,
    ROUND(
        100.0 * COUNT(CASE
            WHEN Rating_Clean IN ('1', '2') THEN 1
        END)
        / NULLIF(COUNT(CASE
            WHEN Rating_Clean IN ('1', '2', '3', '4', '5') THEN 1
        END), 0),
        2
    ) AS negative_feedback_rate
FROM customer_feedback
GROUP BY COALESCE(Category_Clean, 'Missing')
ORDER BY negative_feedback_rate DESC;


-- 7. Overall resolution status distribution
SELECT
    COALESCE(ResolutionStatus_Clean, 'Missing') AS resolution_status,
    COUNT(*) AS feedback_count,
    ROUND(
        100.0 * COUNT(*) /
        (SELECT COUNT(*) FROM customer_feedback),
        2
    ) AS percentage
FROM customer_feedback
GROUP BY COALESCE(ResolutionStatus_Clean, 'Missing')
ORDER BY feedback_count DESC;


-- 8. Resolution rate by category
SELECT
    COALESCE(Category_Clean, 'Missing') AS category,
    COUNT(*) AS total_feedback,
    SUM(CASE
        WHEN ResolutionStatus_Clean = 'Resolved' THEN 1
        ELSE 0
    END) AS resolved_feedback,
    ROUND(
        100.0 * SUM(CASE
            WHEN ResolutionStatus_Clean = 'Resolved' THEN 1
            ELSE 0
        END) / NULLIF(COUNT(*), 0),
        2
    ) AS resolution_rate
FROM customer_feedback
GROUP BY COALESCE(Category_Clean, 'Missing')
ORDER BY resolution_rate ASC;


-- 9. Satisfaction by communication channel
SELECT
    Channel_Clean AS channel,
    COUNT(*) AS total_feedback,
    COUNT(CASE
        WHEN Rating_Clean IN ('1', '2', '3', '4', '5') THEN 1
    END) AS rated_feedback,
    ROUND(AVG(CASE
        WHEN Rating_Clean IN ('1', '2', '3', '4', '5')
        THEN CAST(Rating_Clean AS INTEGER)
    END), 2) AS average_rating
FROM customer_feedback
GROUP BY Channel_Clean
ORDER BY average_rating DESC;


-- 10. Resolution rate by communication channel
SELECT
    Channel_Clean AS channel,
    COUNT(*) AS total_feedback,
    SUM(CASE
        WHEN ResolutionStatus_Clean = 'Resolved' THEN 1
        ELSE 0
    END) AS resolved_feedback,
    ROUND(
        100.0 * SUM(CASE
            WHEN ResolutionStatus_Clean = 'Resolved' THEN 1
            ELSE 0
        END) / NULLIF(COUNT(*), 0),
        2
    ) AS resolution_rate
FROM customer_feedback
GROUP BY Channel_Clean
ORDER BY resolution_rate DESC;


-- 11. Feedback date range
-- Date_Clean is stored as DD/MM/YYYY text.
SELECT
    MIN(
        SUBSTR(Date_Clean, 7, 4) || '-' ||
        SUBSTR(Date_Clean, 4, 2) || '-' ||
        SUBSTR(Date_Clean, 1, 2)
    ) AS earliest_date,
    MAX(
        SUBSTR(Date_Clean, 7, 4) || '-' ||
        SUBSTR(Date_Clean, 4, 2) || '-' ||
        SUBSTR(Date_Clean, 1, 2)
    ) AS latest_date
FROM customer_feedback;


-- 12. Monthly feedback volume
SELECT
    SUBSTR(Date_Clean, 7, 4) || '-' ||
    SUBSTR(Date_Clean, 4, 2) AS feedback_month,
    COUNT(*) AS total_feedback
FROM customer_feedback
GROUP BY feedback_month
ORDER BY feedback_month;


-- 13. Monthly customer satisfaction trends
SELECT
    SUBSTR(Date_Clean, 7, 4) || '-' ||
    SUBSTR(Date_Clean, 4, 2) AS feedback_month,
    COUNT(CASE
        WHEN Rating_Clean IN ('1', '2', '3', '4', '5') THEN 1
    END) AS rated_feedback,
    ROUND(AVG(CASE
        WHEN Rating_Clean IN ('1', '2', '3', '4', '5')
        THEN CAST(Rating_Clean AS INTEGER)
    END), 2) AS average_rating,
    ROUND(
        100.0 * COUNT(CASE
            WHEN Rating_Clean IN ('4', '5') THEN 1
        END)
        / NULLIF(COUNT(CASE
            WHEN Rating_Clean IN ('1', '2', '3', '4', '5') THEN 1
        END), 0),
        2
    ) AS positive_feedback_rate
FROM customer_feedback
GROUP BY feedback_month
ORDER BY feedback_month;


-- 14. Satisfaction by resolution status
SELECT
    COALESCE(ResolutionStatus_Clean, 'Missing') AS resolution_status,
    COUNT(*) AS total_feedback,
    COUNT(CASE
        WHEN Rating_Clean IN ('1', '2', '3', '4', '5') THEN 1
    END) AS rated_feedback,
    ROUND(AVG(CASE
        WHEN Rating_Clean IN ('1', '2', '3', '4', '5')
        THEN CAST(Rating_Clean AS INTEGER)
    END), 2) AS average_rating,
    ROUND(
        100.0 * COUNT(CASE
            WHEN Rating_Clean IN ('4', '5') THEN 1
        END)
        / NULLIF(COUNT(CASE
            WHEN Rating_Clean IN ('1', '2', '3', '4', '5') THEN 1
        END), 0),
        2
    ) AS positive_feedback_rate
FROM customer_feedback
GROUP BY COALESCE(ResolutionStatus_Clean, 'Missing')
ORDER BY average_rating DESC;


-- ============================================================
-- END OF ANALYSIS
-- ============================================================
