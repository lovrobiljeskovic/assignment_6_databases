# assignment_6_databases


**Exercise 1**

```
select customers.customerNumber, employees.employeeNumber, offices.city
from customers, employees, offices
where offices.officeCode = employees.officeCode 
and offices.city = customers.city
;
```

![alt text](https://raw.githubusercontent.com/lovrobiljeskovic/assignment_6_databases/master/exercise1.png)


**Exercise 2**

```
ALTER TABLE `classicmodels`.`customers` 
ADD INDEX `cityIndex` (`city` ASC);
```


**Exercise 3**

##grouping

```
select offices.city, sum(payments.amount), max(payments.amount)
from payments, customers, employees, offices
where payments.customerNumber = customers.customerNumber
and customers.salesRepEmployeeNumber = employees.employeeNumber
and employees.officeCode = offices.officeCode
group by employees.officeCode
;
```

![alt text](https://raw.githubusercontent.com/lovrobiljeskovic/assignment_6_databases/master/exercise3_1.0.png)

##windowing

```
select offices.city,
sum(payments.amount) over (partition by offices.city) as saleAmount,
max(payments.amount) over (partition by offices.city) as maxSale
from payments, customers, employees, offices
where payments.customerNumber = customers.customerNumber
and customers.salesRepEmployeeNumber = employees.employeeNumber
and employees.officeCode = offices.officeCode
```

![alt text](https://raw.githubusercontent.com/lovrobiljeskovic/assignment_6_databases/master/exercise3_2.0.png)


A group by normally reduces the number of rows returned by rolling them up and calculating averages or sums for each row.  partition by does not affect the number of rows returned, but it changes how a window function's result is calculated.


**Exercise 4**

```
select posts.Title, users.DisplayName
from posts, users
where posts.OwnerUserId = users.Id
and posts.Title like("%grounds%")
;
```

![alt text](https://raw.githubusercontent.com/lovrobiljeskovic/assignment_6_databases/master/exercise4.png)


There is no cost in joining because OwnerUserId is index


**Exercise 5**

```
select posts.Title, users.DisplayName
from posts, users
where posts.OwnerUserId = users.Id
and match(title) against ("grounds")
;

alter table posts
add fulltext(title)
;
```

![alt text](https://raw.githubusercontent.com/lovrobiljeskovic/assignment_6_databases/master/exercise5.png)





