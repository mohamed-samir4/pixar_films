create database pixar;

use pixar;

show tables;

set sql_safe_updates = 0;

select * from academy;

-- Format all monetary values in millions------------------------>

select * from box_office;

UPDATE box_office
SET budget = ROUND(budget / 1000000, 1)
WHERE budget IS NOT NULL;

UPDATE box_office
SET box_office_us_canada = ROUND(box_office_us_canada / 1000000, 1)
WHERE box_office_us_canada IS NOT NULL;

UPDATE box_office
SET box_office_other = ROUND(box_office_other / 1000000, 1)
WHERE box_office_other IS NOT NULL;

UPDATE box_office
SET box_office_worldwide = ROUND(box_office_worldwide / 1000000, 1)
WHERE box_office_worldwide IS NOT NULL;

  
select * from box_office;


-- Format percentages with one decimal point------------------------------->


select * from public_response;

alter table public_response
modify column rotten_tomatoes_score varchar(25);

update public_response
set rotten_tomatoes_score = concat(round(rotten_tomatoes_score,1),'%');

alter table public_response
modify column metacritic_score varchar(25);

update public_response
set metacritic_score = concat(round(metacritic_score,1),'%');


select * from public_response;

-- ----------------------------------------------------------------------------------------------------------------------

-- questions ------------------------------------------>

-- task 1 : Financial Performance------->

alter table box_office
add column ROL int;

select * from box_office;

update box_office 
set ROL = ((box_office_worldwide - budget) / budget) * 100;

alter table box_office
modify column ROL varchar(25);

update box_office
set ROL = concat(round(ROL,1),'%');

select * from box_office;



select * from pixar__films;


SELECT 
    pf.film ,
    YEAR (str_to_date(pf.release_date , '%m/%d/%Y')) as release_year,
    bo.budget,
    bo.box_office_worldwide ,
    bo.ROL
FROM pixar__films pf
JOIN box_office bo ON pf.film = bo.film
-- WHERE bo.budget IS NOT NULL AND bo.budget != 0
ORDER BY ROL DESC;


-- -----------------------------------------------------------------------------------

--  task 2 : Award Analysis ----------------------->

SELECT 
    film,
    SUM(CASE WHEN status = 'won' 
		THEN 1 ELSE 0 END) AS awards_won,
    COUNT(*) AS total_nominations,
   concat( ROUND(SUM(CASE WHEN status = 'won' THEN 1 ELSE 0 END) * 100.0 / COUNT(*), 1) , '%')as win_percentage
FROM academy
GROUP BY film
HAVING awards_won > 0
ORDER BY win_percentage DESC;

-- ---------------------------------------------------------------------------------

--  task 3 : Genre Profitability----------------------->

SELECT 
    g.value AS subgenre,
    ROUND(AVG(bo.box_office_worldwide), 1) AS avg_worldwide_million,
    COUNT(*) AS film_count
FROM genres g
JOIN box_office bo ON g.film = bo.film
WHERE bo.box_office_worldwide IS NOT NULL
GROUP BY g.value
HAVING COUNT(*) >= 3
ORDER BY avg_worldwide_million DESC
LIMIT 5;

-- ---------------------------------------------------------------------------------

--  task 4 : Director Impact Study----------------------->

SELECT 
    pp.name AS director_name,
    ROUND(AVG(pr.rotten_tomatoes_score), 1) AS avg_rotten_score,
    ROUND(AVG(bo.box_office_worldwide), 1) AS avg_worldwide_million,
    ROUND(AVG(pr.imdb_score), 1) AS avg_imdb_score
FROM pixar_people pp
JOIN public_response pr ON pp.film = pr.film
JOIN box_office bo ON pp.film = bo.film
WHERE pp.role_type = 'director'
  AND pr.rotten_tomatoes_score IS NOT NULL
  AND pr.imdb_score IS NOT NULL
  AND bo.box_office_worldwide IS NOT NULL
GROUP BY pp.name
HAVING COUNT(DISTINCT pp.film) >= 2
ORDER BY avg_worldwide_million DESC;

-- ---------------------------------------------------------------------------------

--  task 5 : Franchise Comparison----------------------->

SELECT 
    CASE 
        WHEN pf.film LIKE 'Toy Story%' THEN 'Toy Story'
        WHEN pf.film LIKE 'Cars%' THEN 'Cars'
        WHEN pf.film LIKE 'Finding Nemo%' OR pf.film LIKE 'Finding Dory%' THEN 'Finding Nemo/Dory'
    END AS franchise,
    COUNT(*) AS total_films,
    ROUND(SUM(bo.box_office_worldwide), 1) AS total_worldwide_million,
    ROUND(AVG(pf.run_time), 1) AS avg_runtime
FROM pixar__films pf
JOIN box_office bo ON pf.film = bo.film
WHERE 
    pf.film LIKE 'Toy Story%' 
    OR pf.film LIKE 'Cars%' 
    OR pf.film LIKE 'Finding Nemo%' 
    OR pf.film LIKE 'Finding Dory%'
GROUP BY franchise
ORDER BY total_worldwide_million DESC;


-- ---------------------------------------------------------------------------------

--  task 6 : Budget Category Analysis----------------------->

SELECT 
    CASE 
        WHEN bo.budget < 100 THEN 'Low'
        WHEN bo.budget BETWEEN 100 AND 150 THEN 'Medium'
        WHEN bo.budget > 150 THEN 'High'
    END AS budget_category,
    ROUND(AVG(pr.metacritic_score), 1) AS avg_metacritic_score,
    ROUND(AVG(bo.box_office_worldwide), 1) AS avg_worldwide_million,
    COUNT(*) AS film_count
FROM box_office bo
JOIN public_response pr ON bo.film = pr.film
WHERE 
    bo.budget IS NOT NULL 
    AND pr.metacritic_score IS NOT NULL
GROUP BY budget_category
ORDER BY FIELD(budget_category, 'High', 'Medium', 'Low');




















