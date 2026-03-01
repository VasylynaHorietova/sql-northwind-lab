# Task1-Northwind



Define the query for each task. Copy it and the result (screenshot) to the .doc file. Uploa file to this repo

1.	Show all info about the employee with ID 8.
```
select * 
from employees
where employee_id = 8
```
<img width="678" height="48" alt="image" src="https://github.com/user-attachments/assets/ea5f1b08-0c31-493c-b61c-de788db1ffd1" />

2.	
3.	Show the list of first and last names of the employees from London.
```
select FirstName, LastName
from employees
where city like 'London';
```
<img width="186" height="125" alt="image" src="https://github.com/user-attachments/assets/e36801fa-2628-4e40-bbb6-40a319f9e2c0" />

4.	Show the list of first and last names of the employees whose first name begins with letter A.
```
select *
from employees e
where e.FirstName like 'A%';
```
<img width="678" height="73" alt="image" src="https://github.com/user-attachments/assets/1d4c5d52-7404-421f-b21b-23ead855e35b" />

5.	Show the list of first, last names and ages of the employees whose age is greater than 55. The result should be sorted by last name.
```
select 
    FirstName, 
    LastName, 
    (strftime('%Y', 'now') - strftime('%Y', BirthDate)) - (strftime('%m-%d', 'now') < strftime('%m-%d', BirthDate)) AS Age
from employees
where Age > 55
order by Lastname asc;
```
<img width="260" height="78" alt="image" src="https://github.com/user-attachments/assets/c0d95f87-5975-4703-9edf-159d25220804" />
P.S.: It seems that there are no employees older than 55. But the query works correctly, you just need to change the age tj 45 f.e.:
<img width="256" height="106" alt="image" src="https://github.com/user-attachments/assets/f166f52b-0876-4b6b-aff1-b45a0351401f" />

6.	Calculate the count of employees from London.
```
select count(*) as EmployeeCount
from employees
where City='London';
```
<img width="256" height="106" alt="image" src="https://github.com/user-attachments/assets/41558fa2-c85a-42c6-832e-5deaa975b8ea" />

7.	Calculate the greatest, the smallest and the average age among the employees from London.
```
select
max(strftime('%Y', 'now') - strftime('%Y', BirthDate)) AS MaxAge,
min(strftime('%Y', 'now') - strftime('%Y', BirthDate)) AS MinAge,
avg(strftime('%Y', 'now') - strftime('%Y', BirthDate)) AS AvgAge
from employees
where city like 'London';
```
<img width="256" height="106" alt="image" src="https://github.com/user-attachments/assets/4c83a711-6e88-402f-834d-30ec319e2e99" />

8.	Calculate the greatest, the smallest and the average age of the employees for each city.
```
select city,
max(strftime('%Y', 'now') - strftime('%Y', BirthDate)) AS MaxAge,
min(strftime('%Y', 'now') - strftime('%Y', BirthDate)) AS MinAge,
avg(strftime('%Y', 'now') - strftime('%Y', BirthDate)) AS AvgAge
from employees
group by City;
```
<img width="288" height="175" alt="image" src="https://github.com/user-attachments/assets/24f1520f-44ef-4bdb-9bce-f202705dd2a5" />

9.	Show the list of cities in which the average age of employees is greater than 60 (the average age is also to be shown)
```
select city,
avg(strftime('%Y', 'now') - strftime('%Y', BirthDate)) AS AvgAge
from employees
group by City
having AvgAge > 60;
```
<img width="288" height="175" alt="image" src="https://github.com/user-attachments/assets/b159f5c8-cf1f-4b3c-940b-3b63d00ec529" />

10.	Show the first and last name(s) of the eldest employee(s). Use a subquery.
```
select FirstName, LastName
from employees
where Birthdate = (select min(Birthdate) from employees);
```
<img width="288" height="175" alt="image" src="https://github.com/user-attachments/assets/b49508e6-fa2a-4fbc-9cbf-56bf9c748af6" />

11.	Show first, last names and ages of 3 eldest employees.
```
select FirstName, LastName,
(strftime('%Y', 'now') - strftime('%Y', BirthDate)) as Age
from employees
order by BirthDate asc
limit 3;
```
<img width="288" height="175" alt="image" src="https://github.com/user-attachments/assets/9baccc0e-6b79-4deb-83e4-77de7961c049" />

12.	Show the list of all cities where the employees are from.
```
select distinct city from employees;
```
<img width="288" height="175" alt="image" src="https://github.com/user-attachments/assets/5f36ff81-c1f4-44c7-840d-cfcdde72d936" />

13.	Show first, last names and dates of birth of the employees who celebrate their birthdays this month.
```
select FirstName, LastName, Birthdate
from employees
where strftime('%m', BirthDate) = strftime('%m', 'now');
```
<img width="274" height="80" alt="image" src="https://github.com/user-attachments/assets/0a2bb820-dac5-40a4-954b-89012c597f0f" />

14.	Show first and last names of the employees who used to serve orders shipped to Madrid.
```
select distinct e.FirstName, e.LastName
from employees e
join orders o on e.EmployeeID = o.EmployeeID
where o.ShipCity = 'Madrid';
```
<img width="225" height="135" alt="image" src="https://github.com/user-attachments/assets/a66039ce-887c-4585-b15e-7934a8e2e1dc" />

15.	Show first and last names of the employees as well as the count of orders each of them have received during the year 1997 (use left join).
```
select distinct e.FirstName, e.LastName,
count(o.OrderID) as OrderCount
from employees e
left join orders o on e.EmployeeID = o.EmployeeID
and o.OrderDate like '1997%'
group by e.EmployeeID;
```
<img width="282" height="295" alt="image" src="https://github.com/user-attachments/assets/a1079141-547a-49ad-9852-cffab9240105" />

16.	Show first and last names of the employees as well as the count of orders each of them have received during the year 1997 (use a subquery).
```
select e.Firstname, e.LastName,
(select count(*) from orders o
where o.EmployeeID = e.EmployeeID and o.OrderDate like '1997%') as OrderCount
from employees e;
```
<img width="282" height="295" alt="image" src="https://github.com/user-attachments/assets/77168547-af1e-4f48-b480-01ca430d0703" />

17.	Show first and last names of the employees as well as the count of their orders shipped after required date during the year 1997 (use left join).
```
select e.Firstname, e.LastName,
count(o.OrderID) as LateOrders
from employees e
left join orders o on e.EmployeeID = o.EmployeeID
and o.OrderDate like '2014%'
and o.ShippedDate > o.RequiredDate
group by e.EmployeeID;
```
<img width="303" height="293" alt="image" src="https://github.com/user-attachments/assets/2b822dd4-2472-473f-bb8d-3f4a02e583fb" />
P.S.: I replaced 1997 with 2014 because there are no orders for 1997 in the database.

18.	Show the count of orders made by each customer from France.
```
select ContactName, count(OrderID) as OrderCount
from customers c
left join orders o on c.CustomerID = o.CustomerID
where c.Country = 'France'
group by c.CustomerID;
```
<img width="303" height="293" alt="image" src="https://github.com/user-attachments/assets/3868e824-747e-466c-a9b0-468c10f87368" />

19.	Show the list of french customers’ names who have made more than one order (use grouping).
```
select ContactName
from customers c
join orders o on c.CustomerID = o.CustomerID
where c.Country = 'France'
group by c.CustomerID
having count(o.OrderID) > 1;
```
<img width="303" height="293" alt="image" src="https://github.com/user-attachments/assets/c58eae4b-4e18-4dc5-bcad-c5c470307d5f" />

20.	Show the list of french customers’ names who have made more than one order (use a subquery).
```
select ContactName
from customers 
where Country = 'France'
and CustomerID in (
select CustomerID
from orders
group by CustomerID
having count(OrderID) > 1);
```
<img width="303" height="293" alt="image" src="https://github.com/user-attachments/assets/cebaaadc-2a37-4d66-889d-d5a46d152d26" />

21.	Show the list of customers’ names who used to order the ‘Tofu’ product (use a subquery).
```
select ContactName
from customers 
where CustomerID in (
select o.CustomerID
from orders o
join 'Order Details' od on o.OrderID = od.OrderID
join products p on od.ProductID = p.ProductID
where p.ProductName = 'Tofu');
```
<img width="189" height="449" alt="image" src="https://github.com/user-attachments/assets/ea85d1e9-131c-4428-b415-0b02375af8a1" />

22.	*Show the list of customers’ names who used to order the ‘Tofu’ product, along with the total amount of the product they have ordered and with the total sum for ordered product calculated.
```
select c.ContactName,
sum(od.Quantity) as TotalQuantity,
sum(od.Quantity * od.UnitPrice) as TotalSum
from customers c
join orders o on c.CustomerID = o.CustomerID
join 'Order Details' od on o.OrderID = od.OrderID
join products p on od.ProductID = p.ProductID
where p.ProductName = 'Tofu'
group by c.ContactName;
```
<img width="446" height="449" alt="image" src="https://github.com/user-attachments/assets/c55f7135-fce3-4506-9e89-6210a7555436" />

23.	*Show the list of french customers’ names who used to order non-french products (use left join).
```
select distinct c.ContactName
from customers c
left join orders o on c.CustomerID = o.CustomerID
left join 'Order details' od on o.OrderID = od.OrderID
left join products p on od.ProductID = p.ProductID
left join suppliers s on p.SupplierID = s.SupplierID
where c.Country = 'France'
and s.Country <> 'France';
```
<img width="207" height="275" alt="image" src="https://github.com/user-attachments/assets/c3b2ddc3-b427-4734-a608-d5621cd4179f" />

24.	*Show the list of french customers’ names who used to order non-french products (use a subquery).
```
select ContactName
from customers
where Country = 'France'
and CustomerID in (
select o.CustomerID from orders o
join 'Order details' od on o.OrderID = od.OrderID
join products p on od.ProductID = p.ProductID
join suppliers s on p.SupplierID = s.SupplierID
where s.Country <> 'France');
```
<img width="207" height="275" alt="image" src="https://github.com/user-attachments/assets/2ba2e9f2-6819-41ce-bd15-f156eba3a1f6" />

25.	*Show the list of french customers’ names who used to order french products.
```
select distinct c.ContactName
from customers c
left join orders o on c.CustomerID = o.CustomerID
left join 'Order details' od on o.OrderID = od.OrderID
left join products p on od.ProductID = p.ProductID
left join suppliers s on p.SupplierID = s.SupplierID
where c.Country = 'France' 
and s.Country = 'France';
```
<img width="171" height="134" alt="image" src="https://github.com/user-attachments/assets/32533daf-f516-4a9f-8ea6-c2d8265a7b2c" />

26.	*Show the total ordering sum calculated for each country of customer.
```
select c.Country,
sum(od.Quantity * od.UnitPrice) as TotalSum
from customers c
join orders o on c.CustomerID = o.CustomerID
join 'Order Details' od on o.OrderID = od.OrderID
group by c.Country;
```
<img width="220" height="514" alt="image" src="https://github.com/user-attachments/assets/31adfc95-2796-4ef5-9cdb-dde2d6d2cfa6" />

27.	*Show the total ordering sums calculated for each customer’s country for domestic and non-domestic products separately (e.g.: “France – French products ordered – Non-french products ordered” and so on for each country).
```
select c.Country,
sum(case when s.Country = c.Country then od.Quantity * od.UnitPrice else 0 end) as DomesticProductSum,
sum(case when s.Country <> c.Country then od.Quantity * od.UnitPrice else 0 end) as NonDomesticProductSum
from customers c
join orders o on c.CustomerID = o.CustomerID
join 'Order Details' od on o.OrderID = od.OrderID
join products p on od.ProductID = p.ProductID
join suppliers s on p.SupplierID = s.SupplierID
group by c.Country;
```
<img width="466" height="514" alt="image" src="https://github.com/user-attachments/assets/5b4f01f5-e371-49bb-b0d7-5cba7cbd1444" />

28.	*Show the list of product categories along with total ordering sums calculated for the orders made for the products of each category, during the year 1997.
```
select cat.CategoryName,
sum(od.Quantity * od.UnitPrice) as TotalSum
from categories cat
join products p on cat.CategoryID = p.CategoryID
join 'Order Details' od on p.ProductID = od.ProductID
join orders o on od.OrderID = o.OrderID
group by cat.CategoryName;
```
<img width="301" height="218" alt="image" src="https://github.com/user-attachments/assets/a6256b0e-4afa-447a-9d15-72792d869394" />

29.	*Show the list of product names along with unit prices and the history of unit prices taken from the orders (show ‘Product name – Unit price – Historical price’). The duplicate records should be eliminated. If no orders were made for a certain product, then the result for this product should look like ‘Product name – Unit price – NULL’. Sort the list by the product name.
```
select distinct p.ProductName, p.UnitPrice as CurrentUnitPrice,
od.UnitPrice as HistoricalUnitPrice
from products p
left join 'Order Details' od on p.ProductID = od.ProductID
order by p.ProductName;
```
<img width="558" height="814" alt="image" src="https://github.com/user-attachments/assets/e7fe908e-8978-417e-bf95-6de95f2ee173" />

30.	*Show the list of employees’ names along with names of their chiefs (use left join with the same table).
```
select 
e.Firstname || '' || e.LastName as Employee,
m.FirstName || '' || m.LastName as Chief
from employees e
left join employees m on e.ReportsTo = m.EmployeeID;
```
<img width="279" height="285" alt="image" src="https://github.com/user-attachments/assets/6d8be5d1-3083-4a3c-9000-37704fdeda93" />

31.	*Show the list of cities where employees and customers are from and where orders have been made to. Duplicates should be eliminated.
```
select city from employees
union
select city from customers
union
select shipcity from orders;
```
<img width="428" height="594" alt="image" src="https://github.com/user-attachments/assets/e1db9ea1-6034-4e4e-a777-bf2fb23b7f94" />

