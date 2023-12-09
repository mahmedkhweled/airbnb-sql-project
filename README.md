# airbnb-sql-project
This SQL project aims to delve into the wealth of information available within Airbnb datasets to derive meaningful insights, uncover trends, and enhance our understanding of the dynamic short-term rental market.
```sql
Select * from airbnbproject

--Checking data types

Select column_name,Data_Type
from INFORMATION_SCHEMA.COLUMNS
where TABLE_NAME='airbnbproject'

--Changing data type of 'host_since','id' and 'host_id' columns

Alter Table airbnbproject
Alter Column host_since date


alter table airbnbproject
alter column id bigint


Alter Table airbnbproject
Alter Column host_id int

Select * from airbnbproject

--checking and removing duplicate values

;with rownum as (
select * ,row_number()over(partition by host_id,host_since
,host_name,host_location,latitude,longitude
order by host_id) row_num
from airbnbproject)
Delete  from rownum
where row_num>1-- order by host_id


--populating the 'host_location' column with data from the 'name' column

Update airbnbproject

set host_location=(CONCAT
(substring(LEFT(name,abs(charindex('Â',name)-2)),
charindex('in',name)+3,
len(LEFT(name,abs(charindex('Â',name)-1)))),',',' CA'))

select * from airbnbproject


--Droping 'name'column
Alter Table airbnbproject
Drop column name


--What is the top 10 host_total_listings_count?

select distinct top 10 host_total_listings_count,HOST_ID
,HOST_NAME,host_since from airbnbproject
order by host_total_listings_count desc

--Top 10 most common locations 

Select top 10 host_location,COUNT(*) as locations from airbnbproject
group by host_location
order by locations desc

--host_response_time percentage

Select host_response_time ,count(*) as counting ,round(COUNT(*) * 100.0 / SUM(COUNT(*)) over(),2
)as percentage
from airbnbproject
group by host_response_time
order by counting desc
--63.85% of the hosts are super active 
--92.10% of the hosts will response during one day

--
Select distinct  host_id,host_name,host_location,host_total_listings_count from airbnbproject
order by host_total_listings_count desc

Select distinct top 10  host_total_listings_count,host_id,host_name,host_location from airbnbproject
order by host_total_listings_count desc


--the count and the percentage of every room_type

Select room_type ,count(*) as count ,round(COUNT(*) * 100.0 / SUM(COUNT(*)) OVER(),3)
as percentage
from airbnbproject 
group by room_type
order by count desc

--accommdates with the respect of room_type

select room_type,count(room_type) as count_of_room_type ,
count(accommodates) as count_of_accommodates  ,
round(avg(accommodates),0) as average_accommodates 
from airbnbproject
group by room_type 
order by count_of_accommodates desc

--What is the avg price of every room_type?

Select room_type,round(avg(price),2) as average_price from airbnbproject
group by room_type
order by avg(price) desc 

--What isthe top 10 'host_location' average price?

Select top 10 host_location,ROUND(AVG(price),2) as average_price from airbnbproject
group by host_location
order by average_price desc

--What is the average, min and max price of Los Angeles, CA?(as it is the )

Select host_location,ROUND(AVG(price),2) as average_price,
min(price)as min_price,max(price)as max_price
from airbnbproject
Where host_location='Los Angeles, CA'
group by host_location

--Percentage of instant_bookable

select instant_bookable,count(instant_bookable)total_instant_bookable,
COUNT(*) * 100/ SUM(COUNT(*)) OVER() as percentage from airbnbproject
group by instant_bookable
select* from airbnbproject
select distinct top 10 host_total_listings_count,HOST_ID
,HOST_NAME,host_since from airbnbproject
order by host_total_listings_count desc
```
