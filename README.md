PORTLAND BIKE RENTAL:

1. Create database in PostgreSQL
2. Create tables
3. Upload tables
4. Manipulate data
5. Export new table
6. Upload to Tableau Public desktop software
7. When in Tableau, I created an additional column where I categorized the data as either collected on a weekday or the weekend.
  I used the following formula:
  IF [weekday] < 1 THEN 'weekend'
  ELSEIF  [weekday] > 5 THEN 'weekend'
  ELSE 'weekday' END
8. I created a dashboard which can be filtered by clicking on the various categories such as "year", "season" etc. to explore the data

View dashboard [here](https://public.tableau.com/app/profile/tori.robinson/viz/PortlandBikeRental/Dashboard1)

SQL CODE: 
create DATABASE bike_rental_data;


create table bike_rental_yr_0
(
	dteday DATE,
	season INT,
	yr INT,
	mnth INT,
	hr INT,
	holiday INT,
	weekday INT,
	workingday INT,
	weathersit DECIMAL,
	temp DECIMAL,
	atemp DECIMAL,
	hum DECIMAL,
	windspeed DECIMAL,
	rider_type VARCHAR,
	riders INT
	)
	
SELECT * FROM bike_rental_yr_0;	


create table bike_rental_yr_1
(
	dteday DATE,
	season INT,
	yr INT,
	mnth INT,
	hr INT,
	holiday INT,
	weekday INT,
	workingday INT,
	weathersit DECIMAL,
	temp DECIMAL,
	atemp DECIMAL,
	hum DECIMAL,
	windspeed DECIMAL,
	rider_type VARCHAR,
	riders INT
	)

create table costs
(
	yr INT,
	price DECIMAL,
	COGS DECIMAL
)

with cte as (
SELECT * FROM bike_rental_yr_0
UNION
SELECT * FROM bike_rental_yr_1)


select 
dteday,
season,
a.yr,
weekday,
hr,
rider_type,
riders,
riders * price as revenue,
(riders * price) -COGS as profit,
price,
COGS
from cte a
left join costs b
ON a.yr=b.yr;

 
 
