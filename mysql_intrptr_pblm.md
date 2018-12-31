## MySQL Intrepreter Problem And Solution:
While using mysql intrepreter in Zeppelin, I felt two main problems which are listed below:
 
 Problem: 1) Queries with aggregates functions are not working:

For obtaining particular visualization we need to use some aggregate functions such as sum(), avg(), concat()...etc. But while using these kind of functions, no results are obtained.
Example, I didn't get any results for the following queries:-
* Query for comparing population of particular regions:
```
%mysql
select count( `population`), `state/province` from emp.catalog group by `state/province` limit 1000
```
* Query for combining latitude and lngitude of a particular region in order to get the cordinates of particular locations

```
%mysql
select concat(latitude','longitude) as location from emp.catalog list 1000
```
(I managed to solve this queries problem by making some changes with the schema and values ina column named 'geolocation' whcih already contains cordinates points but its datatype was 'text' and there were opening '(' and closing ')' paranthesis with the values. So first I updated its datatype to varchar and also removed its parantheseis using the following queries in MySql console. )
```
UPDATING DATATYPE FROM TEXT TO VARCHAR:
alter table catalog modify column geolocation varchar(50);
 REMOVING PARANTHASIS:
update catalog set geolocation = replace(geolocation, '(', '');
update catalog set geolocation = replace(geolocation, ')', '');
```

Problem: 2) Taking too much time for uploading large size files:

This is one of the main difficult which I felt when I use `%mysql` interpreter in Zeppelin. It took more than half an day to upload a CSV file of Rapido. While using mysql intrepreter, file are uploaded directly to the Mysql server database.

#Solution:

###SQL using spark intrepretr:

We can do the same sql queries by using the spark intrepreter which is a built in feature of Appache Zeppelin.
In spark intrepreter when we uploaded a CSV file its create a temp table to store that file. ie, it is not uploading files directly into DB server.(`NB:what I understood`). So uploading takes more faster than mysql intrepreter. So the previous 'Catalog.csv' file which contains the data of disaters of a particular region is uploaded into zeppelin using the following code:
```
import org.apache.spark.sql.SQLContext
val df = spark.read.format("csv").option("header", "true").load("/home/user/Downloads/catalog.csv")
df.printSchema()
df.registerTempTable("data")
```
And I run the same sql querries here by using spark intrepreter:
```
%sql
select sum( `population`), `state/province` from data group by `state/province` limit 1000
```
We can also perform the querries with aggregrate functions at here:
```
%sql
select concat(latitude','longitude) as location , city from data limit 100
```

 I aslo tried to upload rapido's dumb file at here and didn't find any time issues at here.
