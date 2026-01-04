-- Verify customers
SELECT TOP 10 * FROM customers;

-- (Historical setup – keep for documentation)
DROP TABLE IF EXISTS orders;
DROP TABLE IF EXISTS products;

SELECT COUNT(*) FROM orders;

DROP TABLE IF EXISTS products;

CREATE TABLE products (
    product_id NVARCHAR(50) NOT NULL,
    product_category_name NVARCHAR(100) NULL,
    product_name_lenght FLOAT NULL,
    product_description_lenght FLOAT NULL,
    product_photos_qty FLOAT NULL,
    product_weight_g FLOAT NULL,
    product_length_cm FLOAT NULL,
    product_height_cm FLOAT NULL,
    product_width_cm FLOAT NULL
);

SELECT COUNT(*) FROM products;

-- Verify all tables
SELECT TOP 5 * FROM customers;
SELECT TOP 5 * FROM orders;
SELECT TOP 5 * FROM order_items;
SELECT TOP 5 * FROM products;
SELECT TOP 5 * FROM payments;
SELECT TOP 5 * FROM reviews;
