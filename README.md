# SQL-WindowsFunctions-Lag
Using lag function in SQL to examine month over month spend

SQL Environment: PGAdmin

-----

-- Drop table
DROP TABLE IF EXISTS monthly_spend_table;

-- create table
CREATE TABLE monthly_spend_table (
	month DATE,
	spend NUMERIC(7,2)
);

-- add data
INSERT INTO monthly_spend_table (month, spend)
VALUES ('2022-01-01', 500.00),
('2022-02-01', 1500.00),
('2022-03-01', 2000.00), 
('2022-04-01', 2700.00), 
('2022-05-01', 2300.00), 
('2022-06-01', 3000.00), 
('2022-07-01', 3500.00), 
('2022-08-01', 3800.00),
('2022-09-01', 4500.00),
('2022-10-01', 6500.00),
('2022-11-01', 7500.00),
('2022-12-01', 9999.00);


-- Comment here
select * from monthly_spend_table;

-- use lag function
SELECT
	month, 
	spend,
	LAG(spend,1) OVER (
		ORDER BY month
	) previous_month_spend
--	(spend - previous_month_spend) change
FROM
	monthly_spend_table;
	

	
	
WITH spend2 AS (
	SELECT
		month, 
		spend,
		LAG(spend,1) OVER (
			ORDER BY month
		) previous_month_spend
	FROM
		monthly_spend_table
)
SELECT 
	month, 
	spend, 
	previous_month_spend,  
	(spend - previous_month_spend) change
FROM 
	spend2;
