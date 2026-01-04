-- Inspect order statuses
SELECT
    order_status,
    COUNT(*) AS total_orders
FROM orders
GROUP BY order_status;

-- Create clean_orders view
CREATE VIEW clean_orders AS
SELECT
    order_id,
    customer_id,
    order_status,
    order_purchase_timestamp,
    order_approved_at,
    order_delivered_customer_date,
    order_estimated_delivery_date
FROM orders
WHERE order_status = 'delivered'
  AND order_delivered_customer_date IS NOT NULL;

-- Verify clean view
SELECT COUNT(*) FROM clean_orders;
SELECT TOP 5 * FROM clean_orders;
