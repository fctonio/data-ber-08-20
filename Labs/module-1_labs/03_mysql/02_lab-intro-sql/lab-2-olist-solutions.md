/*---------------------
 LAB 02
---------------------*/
-- Find the earliest and latest first_contact_date
SELECT
	MIN(first_contact_date),
	MAX(first_contact_date)
FROM marketing_qualified_leads;
	
-- Find the top 3 most frequent origin types for all first_contact_date entries in 2018
SELECT 
	origin
FROM marketing_qualified_leads
WHERE first_contact_date >= '2018-01-01'
	AND first_contact_date < '2019-12-31'
GROUP BY origin
ORDER BY COUNT(origin) DESC
LIMIT 3;

-- Find the first_contact_date with the highest number of mql_id entries and state the number of entries on that date.
SELECT 
	first_contact_date,
	COUNT(mql_id)	AS count_mql_id
FROM marketing_qualified_leads
GROUP BY first_contact_date
ORDER BY count_mql_id DESC
LIMIT 1;

-- Find the name and count of the top 2 product category names
SELECT
	product_category_name,
	COUNT(product_category_name) AS count_product_category
FROM products
GROUP BY product_category_name
ORDER BY count_product_category DESC
LIMIT 2;

-- Find the product_category_name with the highest recorded product weight in grams.
SELECT
	product_category_name,
	product_weight_g
FROM products
ORDER BY product_weight_g DESC
LIMIT 1;

-- Find the product_category_name with the greatest sum of dimensions including length, height and width in centimeters.
SELECT 
	product_category_name,
	product_length_cm+product_height_cm+product_width_cm AS total_dimensions
FROM products
ORDER BY total_dimensions DESC
LIMIT 1;

-- Find the payment_type with the greatest number of order_id entries and the count of that payment type
SELECT
	payment_type,
	COUNT(payment_type) AS count_payment_type
FROM order_payments
GROUP BY payment_type
ORDER BY count_payment_type DESC
LIMIT 1;

-- Find the highest payment value for an individual order_id
SELECT
	payment_value
FROM order_payments
ORDER BY payment_value DESC
LIMIT 1;

-- Find the 3 seller states with the greatest number of distinct seller cities
SELECT
	seller_state,
	COUNT(DISTINCT seller_city) AS seller_city_counter
FROM sellers
GROUP BY seller_state
ORDER BY seller_city_counter DESC 
LIMIT 3;