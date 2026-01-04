--Purpose : Business Growth Trends

-- Monthly orders
SELECT
    DATEFROMPARTS(
        YEAR(order_purchase_timestamp),
        MONTH(order_purchase_timestamp),
        1
    ) AS order_month,
    COUNT(DISTINCT order_id) AS total_orders
FROM clean_orders
GROUP BY
    DATEFROMPARTS(
        YEAR(order_purchase_timestamp),
        MONTH(order_purchase_timestamp),
        1
    )
ORDER BY order_month;

-- Monthly revenue
SELECT
    DATEFROMPARTS(
        YEAR(o.order_purchase_timestamp),
        MONTH(o.order_purchase_timestamp),
        1
    ) AS order_month,
    SUM(oi.price + oi.freight_value) AS revenue
FROM clean_orders o
JOIN order_items oi
    ON o.order_id = oi.order_id
GROUP BY
    DATEFROMPARTS(
        YEAR(o.order_purchase_timestamp),
        MONTH(o.order_purchase_timestamp),
        1
    )
ORDER BY order_month;
