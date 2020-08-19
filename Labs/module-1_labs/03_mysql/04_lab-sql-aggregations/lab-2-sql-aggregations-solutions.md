/*--------
LAB 04
--------*/

-- Of all districts with a district_id lower than 10, how many clients are from each district_id? Show the results sorted by district_id in ascending order

SELECT
	district_id,
	COUNT(client_ID) AS clients
FROM client
WHERE district_id < 10
GROUP BY district_id
ORDER BY district_id ASC;

-- How many cards exist for each type? Rank the result starting with the most frequent type.
SELECT 
	type,
	COUNT(card_id) AS number_of_cards
FROM card
GROUP BY type
ORDER BY number_of_cards DESC;

-- Print the top 10 account_ids based on the sum of all of their loan amounts
SELECT
	account_id,
	sum(amount) AS amount_sum
FROM loan
GROUP BY account_id
ORDER BY amount_sum DESC
LIMIT 10;

-- Retrieve the number of loans issued for each day, before (excl) 930907, ordered by date in descending order
SELECT 
	date,
	COUNT(loan_id) AS number_of_loans
FROM loan
WHERE date < '930907'
GROUP BY date
ORDER BY date DESC;

-- For each day in December 1997, count the number of loans issued for each unique loan duration, ordered by date and duration, both in ascending order. You can ignore days without any loans in your output.
SELECT 
	date,
	duration,
	COUNT(loan_id) AS number_of_loans
FROM loan
WHERE date >= '971200'
	AND date < '980000'
GROUP BY date, duration
ORDER BY date ASC;

--  For account_id 396, sum the amount of transactions for each type (VYDAJ = Outgoing, PRIJEM = Incoming). Your output should have the account_id, the type and the sum of amount, named as total_amount. Sort alphabetically by type
SELECT 
	 account_id,
	 type,
	 sum(amount) AS total_amount
FROM trans 
WHERE account_id = '396'
GROUP BY type
ORDER BY type ASC;

-- Translate the values for type to English, rename the column to transaction_type, round total_amount down to an integer
SELECT 
	 account_id,
	 IF(type = 'VYDAJ', 'Outgoing', 'Incoming') as transaction_type,
	 floor(sum(amount)) AS total_amount
FROM trans 
WHERE account_id = '396'
GROUP BY type
ORDER BY type ASC;

-- Modify you query so that it returns only one row, with a column for incoming amount, outgoing amount and the difference
SELECT
	account_id, 
	sum(CASE
	WHEN type = 'PRIJEM' THEN total_amount
	END) AS incoming,
	sum(CASE
	WHEN type = 'VYDAJ' THEN total_amount
	END) AS outgoing,
	sum(CASE
	WHEN type = 'PRIJEM' THEN total_amount
	END) - sum(CASE
	WHEN type = 'VYDAJ' THEN total_amount
	END) AS difference
FROM (
    	SELECT 
	 		account_id,
	 		type,
	 		floor(sum(amount)) AS total_amount
		FROM trans 
		WHERE account_id = '396'
		GROUP BY type
		ORDER BY type ASC
) summary
GROUP BY account_id;
	
-- Rank the top 10 account_ids based on their difference

SELECT
	account_id, 
	sum(CASE
	WHEN type = 'PRIJEM' THEN total_amount
	END) - sum(CASE
	WHEN type = 'VYDAJ' THEN total_amount
	END) AS difference
FROM (
    	SELECT 
	 		account_id,
	 		type,
	 		floor(sum(amount)) AS total_amount
		FROM trans 
		GROUP BY type, account_id
		ORDER BY type ASC
) summary
GROUP BY account_id
ORDER BY difference DESC
LIMIT 10;