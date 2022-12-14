SELECT COUNT(status)
FROM company 
WHERE status = 'closed'

SELECT 	
   funding_total
FROM company
WHERE category_code = 'news' AND country_code ='USA' --AND funding_total <>'0'

ORDER BY funding_total DESC;

SELECT SUM(price_amount) 
FROM acquisition
WHERE term_code = 'cash'  
  AND acquired_at >='2011-01-01' AND acquired_at <='2013-12-31';

SELECT first_name,
   last_name,
   twitter_username
FROM people
WHERE twitter_username LIKE 'Silver%';


SELECT*
FROM people AS p 
WHERE twitter_username LIKE '%money%' 
    AND last_name LIKE 'K%'


SELECT country_code,
    SUM(funding_total)     
FROM  company 
GROUP BY country_code
ORDER  BY SUM(funding_total) DESC;



SELECT funded_at,
   MAX(raised_amount),
   MIN(raised_amount)
FROM funding_round
GROUP BY funded_at
HAVING MIN(raised_amount)<>0
   AND MIN(raised_amount)<> MAX(raised_amount);


SELECT *,
      CASE
          WHEN invested_companies>=100 THEN 'high_activity'
          WHEN invested_companies<100 
          AND invested_companies>= 20 THEN 'middle_activity'
          ELSE 'low_activity'
      END
FROM fund;


WITH
a AS (SELECT *,
       CASE
           WHEN invested_companies>=100 THEN 'high_activity'
           WHEN invested_companies>=20 THEN 'middle_activity'
           ELSE 'low_activity'
       END AS activity
FROM fund)
SELECT activity,
   ROUND(AVG(investment_rounds),0)
FROM a
GROUP BY activity
ORDER BY  ROUND(AVG(investment_rounds),0);


SELECT country_code,
    MIN(invested_companies),
    MAX(invested_companies),
    AVG(invested_companies)
FROM fund
WHERE EXTRACT (YEAR FROM founded_at) BETWEEN 2010 AND 2012     
GROUP BY country_code
HAVING MIN(invested_companies)>0 
ORDER BY AVG DESC 
LIMIT(10)


SELECT first_name,
      last_name,
      instituition
FROM people AS p
LEFT JOIN education AS e ON e.person_id = p.id


WITH
i AS (SELECT p.company_id,      
      instituition
FROM people AS p
LEFT JOIN education AS e ON e.person_id = p.id)

SELECT name,
   COUNT(DISTINCT instituition)
FROM company AS c
LEFT JOIN i ON c.id = i.company_id
GROUP BY name
ORDER BY COUNT DESC
LIMIT(5)


SELECT DISTINCT c.name
FROM company AS c
RIGHT JOIN 
(SELECT*
FROM funding_round AS fr
WHERE is_first_round>0
    AND is_first_round = is_last_round) AS r ON c.id = r.company_id
WHERE status = 'closed'



WITH
cf AS(SELECT DISTINCT c.name,c.id
FROM company AS c
RIGHT JOIN 
(SELECT*
FROM funding_round AS fr
WHERE is_first_round>0
    AND is_first_round = is_last_round) AS r ON c.id = r.company_id
WHERE status = 'closed')

SELECT DISTINCT p.id
FROM people AS p
JOIN cf ON p.company_id = cf.id


WITH
cf AS(SELECT DISTINCT c.name,c.id
FROM company AS c
RIGHT JOIN 
(SELECT*
FROM funding_round AS fr
WHERE is_first_round>0
    AND is_first_round = is_last_round) AS r ON c.id = r.company_id
WHERE status = 'closed')

SELECT  DISTINCT p.id ,
         e.instituition               
FROM people AS p
JOIN cf ON p.company_id = cf.id
INNER JOIN education AS e ON p.id = e. person_id


WITH
cf AS(SELECT DISTINCT c.name,c.id
FROM company AS c
RIGHT JOIN 
(SELECT*
FROM funding_round AS fr
WHERE is_first_round>0
    AND is_first_round = is_last_round) AS r ON c.id = r.company_id
WHERE status = 'closed')

SELECT  DISTINCT p.id ,
         COUNT(e.instituition)               
FROM people AS p
JOIN cf ON p.company_id = cf.id
INNER JOIN education AS e ON p.id = e. person_id
GROUP BY p.id


WITH
cf AS(SELECT DISTINCT c.name,c.id
FROM company AS c
RIGHT JOIN 
(SELECT*
FROM funding_round AS fr
WHERE is_first_round>0
    AND is_first_round = is_last_round) AS r ON c.id = r.company_id
WHERE status = 'closed')

SELECT AVG(best_people.count)

FROM
(SELECT  DISTINCT p.id ,
         COUNT(e.instituition)               
FROM people AS p
JOIN cf ON p.company_id = cf.id
INNER JOIN education AS e ON p.id = e. person_id
GROUP BY p.id) AS best_people


SELECT AVG(fcb.count_instituition) AS avg_count_instituition
FROM
(SELECT DISTINCT p.id AS id_people,
         COUNT(instituition) AS count_instituition
FROM people AS p
JOIN education AS e ON e.person_id = p.id
WHERE company_id IN (SELECT id
FROM company
WHERE name = 'Facebook')
GROUP BY id_people) AS fcb


SELECT DISTINCT f.name AS name_of_fund,
        c.name AS name_of_company,
        SUM(fr.raised_amount) AS amount
FROM investment AS i
INNER JOIN company AS c ON i.company_id = c.id
INNER JOIN fund AS f ON i.fund_id = f.id
INNER JOIN funding_round AS fr ON i.funding_round_id = fr.id
WHERE c.milestones > 6
   AND EXTRACT (YEAR FROM fr.funded_at) BETWEEN 2012 AND 2013 
GROUP BY f.name, c.name, fr.funding_round_type;  



WITH
one AS
(SELECT a.acquired_company_id,
         c.name AS acquired_company ,
      c.funding_total 
FROM acquisition AS a
LEFT JOIN company AS c ON a.acquired_company_id  =  c.id
WHERE c.funding_total > 0)

SELECT DISTINCT c.name AS acquiring_company ,
       a.price_amount,
       one.acquired_company,
       one.funding_total,
       ROUND(a.price_amount/one.funding_total,0)       
FROM acquisition AS a
LEFT JOIN company AS c ON a.acquiring_company_id  =  c.id
INNER JOIN one ON a.acquired_company_id = one.acquired_company_id 
WHERE a.price_amount >0
ORDER BY a.price_amount DESC,one.acquired_company
LIMIT(10)



SELECT c.name,
       one.month 
FROM company AS c
INNER JOIN
(SELECT company_id , 
       EXTRACT(MONTH FROM funded_at) AS month
FROM funding_round
WHERE EXTRACT(YEAR FROM funded_at) BETWEEN 2010 AND 2013) AS one
ON c.id = one.company_id
WHERE category_code ='social'


WITH
fund AS
(SELECT EXTRACT(MONTH FROM funded_at) AS month,
 COUNT(DISTINCT f.name) AS count_fund
FROM investment  AS i JOIN  fund AS f ON i.fund_id = f.id
JOIN funding_round AS fr ON i.funding_round_id = fr.id
WHERE  EXTRACT(YEAR FROM funded_at) BETWEEN 2010 AND 2013 
 AND f.country_code = 'USA'
 GROUP BY month),

company AS
(SELECT EXTRACT(MONTH FROM acquired_at) AS month,
        COUNT(acquired_company_id)AS count_acquired_company ,
        SUM(price_amount) 
FROM acquisition
WHERE 	EXTRACT(YEAR FROM acquired_at) BETWEEN 2010 AND 2013
GROUP BY month)

SELECT fund.month,
       fund.count_fund,
       company.count_acquired_company,
       company.SUM
FROM fund JOIN company ON fund.month = company.month



WITH
one AS
(SELECT country_code,
      AVG(funding_total) AS year_2011
FROM company  
WHERE EXTRACT(YEAR FROM founded_at )=2011 
   AND country_code IS NOT NULL
GROUP BY country_code),
too AS
(SELECT country_code,
      AVG(funding_total) AS year_2012
FROM company  
WHERE EXTRACT(YEAR FROM founded_at)=2012
   AND country_code IS NOT NULL
GROUP BY country_code),
three AS
(SELECT country_code,
      AVG(funding_total) AS year_2013
FROM company 
WHERE EXTRACT(YEAR FROM founded_at)=2013
   AND country_code IS NOT NULL
GROUP BY country_code)

SELECT one.country_code,
       one.year_2011,
       too.year_2012,
       three.year_2013
FROM one
INNER JOIN too ON one.country_code = too.country_code
INNER JOIN three ON too.country_code = three.country_code
ORDER BY one.year_2011 DESC

