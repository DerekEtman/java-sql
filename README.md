# java-sql

A student that completes this project shows that they can:
* Query data from a single table
* Query data from multiple tables
* Create a new datadaase using PostgreSQL

# Introduction

Working with SQL

# Instructions

ReImport the Northwind database into PostgreSQL using pgAdmin. This is the same data we used during the guided project.

clone https://github.com/pthom/northwind_psql.git

## pgAdmin

* Right Click Databases
  * Create
    * type in northwind2

* Tools -> Query Tool
  * Open file northwind.sql (from cloned repo)
  * Execute

* Look under
  * northwind2 -> Schemas -> public -> tables

* Clear query windows

Answer the following data queries. Keep track of the SQL you write by pasting it into this document under its appropriate header below. You will be submitting that through the regular fork, change, pull process.


### find all customers that live in London. Returns 6 records.
> This can be done with SELECT and WHERE clauses

## Answer:
    SELECT contact_name, country, city
    FROM customers
    WHERE city = 'London'



### find all customers with postal code 1010. Returns 3 customers.
> This can be done with SELECT and WHERE clauses

## Answer:
    'SELECT contact_name, postal_code
    FROM customers
    WHERE postal_code = '1010'



### find the phone number for the supplier with the id 11. Should be (010) 9984510.
> This can be done with SELECT and WHERE clauses

## Answer:
    SELECT supplier_id, contact_name, phone
    FROM suppliers
    WHERE supplier_id = '11'



### list orders descending by the order date. The order with date 1998-05-06 should be at the top.
> This can be done with SELECT, WHERE, and ORDER BY clauses

## Answer:
    SELECT order_date, customer_id
    FROM orders
    WHERE order_date is not null
    ORDER BY order_date desc



### find all suppliers who have names longer than 20 characters. You can use `length(company_name)` to get the length of the name. Returns 11 records.
> This can be done with SELECT and WHERE clauses

## Answer:
    SELECT company_name 
    FROM suppliers
    WHERE LENGTH(company_name) > '20' 



### find all customers that include the word 'MARKET' in the contact title. Should return 19 records.
> This can be done with SELECT and a WHERE clause using the LIKE keyword

> Don't forget the wildcard '%' symbols at the beginning and end of your substring to denote it can appear anywhere in the string in question

> Remember to convert your contact title to all upper case for case insenstive comparing so upper(contact_title)

## Answer:
    SELECT contact_name, company_name
    FROM customers
    WHERE upper(contact_title) LIKE '%MARKET%'



### add a customer record for   
* customer id is 'SHIRE'
* company name is 'The Shire'
* contact name is 'Bilbo Baggins'
* the address is '1 Hobbit-Hole'
* ths city is 'Bag End'
* the postal code is '111'
* the country is 'Middle Earth'
> This can be done with the INSERT INTO clause

## Answer:
    INSERT INTO customers(customer_id, company_name, contact_name, address, city, postal_code, country)
    VALUES ('SHIRE', 'THE SHIRE', 'Bilbo Baggins',  '1 Hobbit-Hole', 'Bag End','111','Middle Earth' )



### update _Bilbo Baggins_ record so that the postal code changes to _"11122"_.
> This can be done with UPDATE and WHERE clauses

## Answer:
    UPDATE customers
    SET postal_code= '11122'
    WHERE contact_name = 'Bilbo Baggins'



### list orders grouped by customer showing the number of orders per customer. _Rattlesnake Canyon Grocery_ should have 18 orders.
> This can be done with SELECT, COUNT, JOIN and GROUP BY clauses. Your count should focus on a field in the Orders table, not the Customer table

> There is more information about the COUNT clause on [W3 Schools](https://www.w3schools.com/sql/sql_count_avg_sum.asp)

## Answer:
    SELECT ship_name, COUNT(*) as ordCount
    FROM orders
    GROUP BY ship_name
    Order BY ordCount Desc



### list customers names and the number of orders per customer. Sort the list by number of orders in descending order. _Save-a-lot Markets should be at the top with 31 orders followed by _Ernst Handle_ with 30 orders. Last should be _Centro comercial Moctezuma_ with 1 order.
> This can be done by adding an ORDER BY clause to the previous answer

## Answer:
    SELECT ship_name, COUNT(*) as ordCount
    FROM orders
    GROUP BY ship_name
    Order BY ordCount Desc



### list orders grouped by customer's city showing number of orders per city. Returns 69 Records with _Aachen_ showing 6 orders and _Albuquerque_ showing 18 orders.
> This is very similar to the previous two queries, however, it focuses on the City rather than the CustomerName

## Answer:
    SELECT ship_name, COUNT(*) as ordCount
    FROM orders
    GROUP BY ship_name



## Data Normalization

Note: This step does not use PostgreSQL!

Take the following data and normalize it into a 3NF database.  You can use the website https://www.tablesgenerator.com/markdown_tables# to help generate Markdown Tables.

| Person Name | Pet Name | Pet Type | Pet Name 2 | Pet Type 2 | Pet Name 3 | Pet Type 3 | Fenced Yard | City Dweller |
|-------------|----------|----------|------------|------------|------------|------------|-------------|--------------|
| Jane        | Ellie    | Dog      | Tiger      | Cat        | Toby       | Turtle     | No          | Yes          |
| Bob         | Joe      | Horse    |            |            |            |            | No          | No           |
| Sam         | Ginger   | Dog      | Miss Kitty | Cat        | Bubble     | Fish       | Yes         | No           |

---

## Answer:
    https://docs.google.com/spreadsheets/d/15mbhwuUEqk-CaHA2kWnFk92umELe4WPD3sSMrOn0nfs/edit?usp=sharing

## Stretch Goals

### delete all customers that have no orders. Should delete 2 (or 3 if you haven't deleted the record added) records.

## Create Database and Table

### After creating the database, tables, columns, and constraint, generate the script necessary to recreate the database. This script is what you will submit for review. 

- use pgAdmin to create a database, naming it `budget`.
- add an `accounts` table with the following _schema_:

  - `id`, numeric value with no decimal places that should autoincrement.
  - `name`, string, add whatever is necessary to make searching by name faster.
  - `budget` numeric value.

- constraints
  - the `id` should be the primary key for the table.
  - account `name` should be unique.
  - account `budget` is required.
