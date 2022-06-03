# My notes 
![image_logo](https://www.ovhcloud.com/sites/default/files/styles/text_media_horizontal/public/2021-09/ECX-1909_Hero_PostgreSQL_600x400%402x.png)

## Create database
```sql
 CREATE DATABASE test_db;
```

## Create table
```sql
 # CREATE TABLE table_name{ column_name + data_type + constraints }
 CREATE TABLE person(
 id INT,
 first_name VARCHAR(50),
 last_name VARCHAR(50),
 gender VARCHAR(7),
 date_of_birth DATE);

 DROP TABLE person;

 CREATE TABLE person_const(
 id BIGSERIAL NOT NULL PRIMARY KEY,
 first_name VARCHAR(50) NOT NULL,
 last_name VARCHAR(50) NOT NULL,
 gender VARCHAR(50) NOT NULL,
 date_of_birth DATE NOT NULL,
 email VARCHAR(150));
```

## Insert records into tables
```sql
 INSERT INTO person_const (first_name, last_name, gender, date_of_birth)
 VALUES ('Anne', 'Smith', 'FEMALE', DATE '1988-01-09');

 INSERT INTO person_const (first_name, last_name, gender, date_of_birth, email)
 VALUES ('Jake', 'Jones', 'MALE', DATE '1988-01-10', 'jake@gmail.com´);
```

## Select from
```sql
 SELECT * FROM person_const;

 #Delete old history
 DROP TABLE person_const;

 #Add new data with querys and execute
 > person_table.sql
```

## Sorting
```sql
 SELECT * FROM person_table ORDER BY country_of_birth ASC | DESC;

 #First nulls (email) after data
 SELECT * FROM person_table ORDER BY id, email DESC;
 SELECT * FROM person_table ORDER BY last_name, country_of_birth DESC;
```

## Removing duplicates
```sql
 SELECT country_of_birth FROM person_table ORDER BY country_of_birth;
 
 #Only one country
 SELECT DISTINCT country_of_birth FROM person_table ORDER BY country_of_birth DESC;

 #122 this case
 SELECT COUNT(DISTINCT country_of_birth) FROM person_table;
```

## Where clause
```sql
 #Conditions 
 SELECT * FROM person_table WHERE gender = 'Female' AND country_of_birth = 'Brazil';

 SELECT * FROM person_table WHERE gender = 'Male' AND(country_of_birth = 'Poland' OR country_of_birth = 'Mexico');
```

## Comparison Operators
```sql
 #Operators "<" ">" "<=" ">=" "=" "<>" "!="
 #Strings, Dates
 #Output: Boolean
 SELECT 1 = 1; /*T*/
 SELECT 2 <> 3; /*T*/
 SELECT 3 != 2; /*T*/
 SELECT 8 >= 10; /*F*/
 
 #Comparison predicates
 # BETWEEN, AND, OR, NOT, IS DISTINCT, IS NULL, IS TRUE, IS FALSE, IS UNKNOWN
 SELECT * FROM person_table WHERE country_of_birth = 'China' OR country_of_birth = 'Brazil' OR country_of_birth = 'France';
 SELECT * FROM person_table WHERE country_of_birth IN ('China', 'Mexico', 'France');

 #Real example
 SELECT * FROM person_table WHERE country_of_birth IN ('Nigeria', 'Mexico', 'France') AND gender='Male' ORDER BY country_of_birth;
```

## Limit Offset and Fetch
```sql
 SELECT * FROM person_table LIMIT 10;

 #Another way
 SELECT * FROM person_table OFFSET 5 LIMIT 10;
 SELECT * FROM person_table OFFSET 5 FETCH  FIRST 10 ROW ONLY;
 
 #One row 
 SELECT * FROM person_table OFFSET 618 FETCH  FIRST ROW ONLY;
```

I'm here 

## Tips and Tricks 
- [Awesome list about PostgreSQL](https://github.com/dhamaniasad/awesome-postgres)

```bash
 #List all db
 /l 

 #Show full available commands
 psql --help 

 #Help
 \h or \? 

 #Quit
 /q

 #List all databases
 /l
 
 #Connect by one line in psql
 psql -h localhost -p 0000 -U username test_db;

 # Connect db
 /c test_db 

 #Show list of relations
 /d

 #Table information
 /d table_name

 #Use mockaroo data
 #Path: 'C:/Users/PC/SQL/person_table.sql'
 \i path\script.sql

 #ASCending [{1 2 3 4 5} {A B C}]
 ASC

 #DESCending [{5 4 3 2 1} {Z Y X}]
 DESC
```
