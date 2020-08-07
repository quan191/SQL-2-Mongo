# SQL-2-Mongo
## Method to convert from sequel query langue to non sequel query langue 
In mongodb , there is a tool name mongoImport , we can use that to create and import csv file to mongodb. 

## Example
* 1 We use this database for example 
![Image of Diagram](https://github.com/quan191/SQL-2-Mongo/blob/master/databasediagram.png?raw=true)

* 2 We use these queries in MySQL Workspace 
![Image of SQL ](https://github.com/quan191/SQL-2-Mongo/blob/master/MySQL.png?raw=true)

* 3 First i create a MongoorderDetail table to import to mongodb. 
```
USE classicmodels;
DROP TABLE IF EXISTS `MongoorderDetail`;

CREATE TABLE `MongoorderDetail` (
  `productCode.0.id` varchar(15) NOT NULL,
  `orderNumber` int(11) NOT NULL,
  `productCode.0.nam` varchar(70) NOT NULL,
  `productCode.0.price` text NOT NULL
) ENGINE=InnoDB DEFAULT CHARSET=latin1;
```
* 4 For example , we use productCode and orderNumber from table orderDetails , productName and buyPrice from products to insert to MongoorderDetail table . then export to test.csv file
```
INSERT INTO MongoorderDetail (`productCode.0.id` , `orderNumber`,`productCode.0.nam`,`productCode.0.price`)
SELECT A.productCode as `productCode.0.id`,
A.orderNumber as `orderNumber`, 
B.productName as `productCode.0.nam` , 
B.buyPrice as `productCode.0.price`
FROM orderdetails as A
JOIN products as B 
ON A.productCode=B.productCode;
```

* 5 Open terminal and use this command line 
```
mongoimport -d testSQL2Mongo -c things --type csv --file test.csv --headerline
```
![Image of terminal ](https://github.com/quan191/SQL-2-Mongo/blob/master/terminal.png?raw=true)

* 6 This is the result in MongoDb , i use robo 3T to show MongoDB database
![Image of terminal ](https://github.com/quan191/SQL-2-Mongo/blob/master/mongo.png?raw=true)




