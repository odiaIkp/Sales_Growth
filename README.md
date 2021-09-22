
USE david;
## to show the view of my table
select* 
from flavors;

##join all together to form table
select
RAY.chocosales,
OSA.week,
MAR.strawsales,
MUM.lemonsales,
OSA.vanisales,
IKP.total_sales
from IKP
inner join RAY ON RAY.week=IKP.week
inner join MAR ON MAR.week=RAY.week
inner join MUM ON MUM.week=MAR.week
inner join OSA ON OSA.week=MUM.week;

## TO GET THE HIGHEST FLAVOR SOLD chocolate=460.lemon=713,vanilla=527, strawsales=399 
CREATE TEMPORARY TABLE RAY
select
week,
units_sold,
flavor,
(
 select
 SUM(units_sold)
from flavors
where flavor='chocolate') as chocosales
from flavors;
##
CREATE TEMPORARY TABLE MAR
select
week,
units_sold,
flavor,
(
 select
 SUM(units_sold)
from flavors
where flavor='strawberry') as strawsales
from flavors;
##
CREATE TEMPORARY TABLE MUM
select
week,
units_sold,
flavor,
(
 select
 SUM(units_sold)
from flavors
where flavor='lemon') as lemonsales
from flavors

###
CREATE TEMPORARY TABLE OSA

select
week,
units_sold,
flavor,
(
 select
 SUM(units_sold)
from flavors
where flavor='vanilla') as vanisales
from flavors;

## to get the total unit sold
CREATE TEMPORARY TABLE IKP

select
week,
units_sold,
flavor,
 (select
  SUM(units_sold)
  from flavors) AS total_sales
  from flavors
