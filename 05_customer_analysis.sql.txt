--Purpose: Customer behavior & retention
-- Customer order summary
SELECT
    c.customer_id,
    MIN(o.order_purchase_timestamp) AS first_order_date,
    COUNT(DISTINCT o.order_id) AS total_orders
FROM customers c
JOIN clean_orders o
    ON c.customer_id = o.customer_id
GROUP BY c.customer_id;

-- Customer segmentation
SELECT
    c.customer_id,
    COUNT(DISTINCT o.order_id) AS total_orders,
    CASE
        WHEN COUNT(DISTINCT o.order_id) = 1 THEN 'New'
        WHEN COUNT(DISTINCT o.order_id) BETWEEN 2 AND 4 THEN 'Repeat'
        ELSE 'Loyal'
    END AS customer_segment
FROM customers c
JOIN clean_orders o
    ON c.customer_id = o.customer_id
GROUP BY c.customer_id;

-- Segment distribution
SELECT
    customer_segment,
    COUNT(*) AS number_of_customers
FROM (
    SELECT
        c.customer_id,
        CASE
            WHEN COUNT(DISTINCT o.order_id) = 1 THEN 'New'
            WHEN COUNT(DISTINCT o.order_id) BETWEEN 2 AND 4 THEN 'Repeat'
            ELSE 'Loyal'
        END AS customer_segment
    FROM customers c
    JOIN clean_orders o
        ON c.customer_id = o.customer_id
    GROUP BY c.customer_id
) t
GROUP BY customer_segment;
