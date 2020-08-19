/*---------------------
 LAB 01
---------------------*/
-- Maximum 

SELECT
	price
FROM olist.order_items
ORDER BY price DESC
LIMIT 1;

-- Minimum
	
SELECT
	price
FROM olist.order_items
ORDER BY price ASC
LIMIT 1;

-- Range 
SELECT MIN(shipping_limit_date), MAX(shipping_limit_date)
FROM olist.order_items;

-- States with greatest number of customers
SELECT 
	customer_state,
	COUNT(customer_state)
FROM olist.customers
GROUP BY customer_state
ORDER BY COUNT(customer_state) DESC
limit 3;

-- Within state with greatest number of customers find 3 cities with most customers

SELECT 
	customer_city,
	COUNT(customer_city)
FROM olist.customers
WHERE customer_state = 'SP'
GROUP BY customer_city
ORDER BY COUNT(customer_city) DESC
limit 3;

-- Clodes deal table, distinct business segments
SELECT
	COUNT(distinct business_segment) AS Number_of_distinct_business_segments
FROM olist.closed_deals;


-- Sum declared_monthly_revenue for duplicate row values in business_segment and find the 3 business segments with the highest declared monthly revenue (of those that declared revenue).
SELECT
	SUM(declared_monthly_revenue) AS Monthly_revenue_by_segment,
	business_segment
FROM closed_deals
GROUP BY business_segment
ORDER BY Monthly_revenue_by_segment DESC 
LIMIT 3;

-- Total number of distinct review score values
SELECT
	COUNT(DISTINCT review_score)
FROM order_reviews;

-- create a new column with a description that corresponds to each number category for each review score from 1 - 5.
SELECT 
	review_id,
	order_id,
	review_score,
	review_comment_title,
	review_comment_message,
	review_creation_date,
	review_answer_timestamp,
	CASE
		WHEN review_score = 1 THEN 'very bad'
		WHEN review_score = 2 THEN 'bad'
		WHEN review_score = 3 THEN 'ok'
		WHEN review_score = 4 THEN 'good'
		ELSE 'very good'
	END AS review_catagory
FROM order_reviews;

-- review score occurring most frequently and how many times it occurs
SELECT
	review_score,
	count(1)		AS review_count
FROM order_reviews
GROUP BY review_score
ORDER BY review_count DESC
LIMIT 1;

