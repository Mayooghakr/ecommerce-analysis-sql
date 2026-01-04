--Purpose: Operations & customer satisfaction

-- Delivery days calculation
SELECT
    o.order_id,
    DATEDIFF(
        DAY,
        o.order_approved_at,
        o.order_delivered_customer_date
    ) AS delivery_days
FROM clean_orders o
WHERE o.order_approved_at IS NOT NULL;

-- Delivery speed buckets
SELECT
    o.order_id,
    CASE
        WHEN DATEDIFF(DAY, o.order_approved_at, o.order_delivered_customer_date) <= 2
            THEN '0–2 days'
        WHEN DATEDIFF(DAY, o.order_approved_at, o.order_delivered_customer_date) <= 5
            THEN '3–5 days'
        ELSE '6+ days'
    END AS delivery_bucket
FROM clean_orders o
WHERE o.order_approved_at IS NOT NULL;

-- Delivery speed vs review score
SELECT
    CASE
        WHEN DATEDIFF(DAY, o.order_approved_at, o.order_delivered_customer_date) <= 2
            THEN '0–2 days'
        WHEN DATEDIFF(DAY, o.order_approved_at, o.order_delivered_customer_date) <= 5
            THEN '3–5 days'
        ELSE '6+ days'
    END AS delivery_bucket,
    COUNT(*) AS total_orders,
    AVG(r.review_score) AS avg_review_score
FROM clean_orders o
JOIN reviews r
    ON o.order_id = r.order_id
WHERE o.order_approved_at IS NOT NULL
GROUP BY
    CASE
        WHEN DATEDIFF(DAY, o.order_approved_at, o.order_delivered_customer_date) <= 2
            THEN '0–2 days'
        WHEN DATEDIFF(DAY, o.order_approved_at, o.order_delivered_customer_date) <= 5
            THEN '3–5 days'
        ELSE '6+ days'
    END
ORDER BY avg_review_score DESC;
