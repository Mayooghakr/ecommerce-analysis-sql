Purpose: Product & category performance

-- Revenue by product category
SELECT
    p.product_category_name,
    SUM(oi.price + oi.freight_value) AS category_revenue
FROM clean_orders o
JOIN order_items oi
    ON o.order_id = oi.order_id
JOIN products p
    ON oi.product_id = p.product_id
GROUP BY p.product_category_name
ORDER BY category_revenue DESC;

-- Handle NULL categories
SELECT
    COALESCE(p.product_category_name, 'Unknown') AS product_category,
    SUM(oi.price + oi.freight_value) AS category_revenue
FROM clean_orders o
JOIN order_items oi
    ON o.order_id = oi.order_id
JOIN products p
    ON oi.product_id = p.product_id
GROUP BY COALESCE(p.product_category_name, 'Unknown')
ORDER BY category_revenue DESC;

-- Top 10 products by revenue
SELECT TOP 10
    oi.product_id,
    SUM(oi.price + oi.freight_value) AS product_revenue
FROM clean_orders o
JOIN order_items oi
    ON o.order_id = oi.order_id
GROUP BY oi.product_id
ORDER BY product_revenue DESC;

-- High-volume, low-revenue products
SELECT TOP 10
    oi.product_id,
    COUNT(DISTINCT o.order_id) AS total_orders,
    SUM(oi.price + oi.freight_value) AS total_revenue
FROM clean_orders o
JOIN order_items oi
    ON o.order_id = oi.order_id
GROUP BY oi.product_id
ORDER BY total_orders DESC;
