/*--------
LAB 03
--------*/
USE bank

-- What are the ids of the first 5 clients from disrict_id 1
SELECT
	client_id
FROM client
ORDER BY district_id, client_id ASC
LIMIT 5;

-- What is the id of the last client from district_id 72
SELECT
	client_id
FROM client
WHERE district_id = '72'
ORDER BY client_id DESC
LIMIT 1;

-- What are the 3 lowest amounts
SELECT 
	amount
FROM loan
ORDER BY amount ASC
LIMIT 3;

-- What are the possible values for status, ordered alphabetically in ascending order
SELECT 
	DISTINCT status 
FROM loan
ORDER BY status ASC;

-- What is the loan_id of the highest payment received
SELECT 
	loan_id
FROM loan
ORDER BY payments DESC
LIMIT 1;

-- What is the loan amount of the lowest 5 account_ids. Show the account_id and the corresponding amount
SELECT
	account_id,
	amount
FROM loan
ORDER BY account_id ASC
LIMIT 5; 

-- Which are the account_ids with the lowest loan amount have a loan duration of 60
SELECT
	account_id
FROM LOAN
WHERE duration = '60'
ORDER BY amount ASC
LIMIT 5;

--  What are the unique values of k_symbol
SELECT
	DISTINCT k_symbol
FROM `order`
ORDER BY k_symbol DESC;

-- Which are the order_ids from the client with the account_id 34
SELECT 
	order_id
FROM `order`
WHERE account_id = '34';

-- Which account_ids were responsible for orders between order_id 29540 and order_id 29560 (inclusive)
SELECT 
	DISTINCT account_id
FROM `order`
WHERE order_id >= "29540"
	AND order_id <= "29560";
	
-- What are the individual amounts that were sent to (account_to) id 30067122
SELECT 
	amount
FROM `order`
WHERE account_to = '30067122';

-- Show the trans_id, date, type and amount of the 10 first transactions from account_id = 793 in chronological order, from newest to oldest
SELECT 
	trans_id,
	date,
	type,
	amount
FROM trans
WHERE account_id = '793'
ORDER BY date DESC
LIMIT 10;