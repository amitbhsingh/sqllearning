use classicmodels;

SELECT customerNumber, CONCAT(customerName,' ',contactLastName) as custfullname, phone,addressLine1
,city,postalCode,salesRepEmployeeNumber
from customers;
select * 
from customers 
where custfullname="%brown%";
# match strings with similar characters
select
customerName,contactLastName,city,
CASE
WHEN LOWER(city) LIKE '%Las%'
then 'local'
else 'other'
end as local_city
from customers
# Selection of data where creditLimit is more than X to be assigned as 1 and otherwize 0
select customerNumber, customerName, creditLimit,
case 
when creditLimit>50000
then 1
else 0
end as priceover50
from customers;
# SQL left joins 
# example “SELECT
# [columns to return]
# FROM
# [left table]
#[JOIN TYPE] [right table]
#ON
# [left table].[field in left table to match] = [right table].[field in right table to match]”


SELECT *
from customers left join employees on customers.salesRepEmployeeNumber=employees.employeeNumber;
#verifying above stated query with the actual data 
select * from customers
where customers.customerNumber=125;
select * from employees
# Joins with more than two table
select c.customerNumber,c.customerName
from customers as c
# Aggregation
select customerName,creditLimit
from customers
order by customers.customerName 

# query to find out the entries where the shipment was shipped on or after required date
select *
from orders
where shippedDate >= requiredDate 
# query to find out the entries where the shipment was shipped after required date 
select *
from orders
where shippedDate>requiredDate
# there is only one order and reason: This order was on hold because customers's credit limit had been exceeded. Order will ship when payment is received

# order by with duplicates
select customerName, creditLimit
from classicmodels.customers
order by customerName,creditLimit
# order by and group by eliminating the duplicates
select  customerName,creditLimit
from classicmodels.customers
group by customerName,creditLimit
order by customerName,creditLimit


select count(salesRepEmployeeNumber) as noofsales, customerName
from customers
group by salesRepEmployeeNumber,customerName

# Count sum of column 
select paymentDate,customerNumber,
sum(amount) as total
from classicmodels.payments
group by paymentDate,customerNumber
order by paymentDate,customerNumber 


