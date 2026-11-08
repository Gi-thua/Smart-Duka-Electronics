## Smart Duka Electronics

Smart Duka Electronics is a SQL database project designed to manage and analyze an electronics retail business. The project consists of two related tables: Customers and Orders, which store customer information, product purchases, sales transactions, and payment details. The database supports sales tracking, customer segmentation, product performance analysis, revenue and profit calculations, and order status monitoring. It demonstrates the practical application of SQL concepts, including table relationships, queries, aggregate functions, joins, views, stored functions, and database performance optimization.

## How to Set Up and Run the Project
- Create the Schema

`create schema electronics;`

- Create the Tables

`CREATE TABLE IF NOT EXISTS customers (
    customer_id        INTEGER      PRIMARY KEY,
    customer_name      VARCHAR(100) NOT NULL,
    gender             VARCHAR(10)  CHECK (gender IN ('Male', 'Female')),
    city               VARCHAR(50),
    registration_date  DATE,
    customer_segment   VARCHAR(20)  CHECK (customer_segment IN ('Retail', 'Corporate', 'VIP'))
);`


`CREATE TABLE IF NOT EXISTS orders (
    order_id          INTEGER       PRIMARY KEY,
    customer_id       INTEGER       NOT NULL REFERENCES customers (customer_id),
    order_date        DATE          NOT NULL,
    product_name      VARCHAR(100),
    product_category  VARCHAR(50),
    quantity          INTEGER       CHECK (quantity > 0),
    unit_price        NUMERIC(12,2) CHECK (unit_price >= 0),
    cost_price        NUMERIC(12,2) CHECK (cost_price >= 0),
    discount          NUMERIC(5,2)  DEFAULT 0 CHECK (discount BETWEEN 0 AND 100),
    payment_method    VARCHAR(30)   CHECK (payment_method IN ('M-Pesa', 'Cash', 'Card', 'Bank Transfer')),
    order_status      VARCHAR(20)   CHECK (order_status IN ('Completed', 'Pending', 'Cancelled'))
);`


- Insert Sample Data
  
I insert SQL INSERT statements to populate both tables with sample customer and order records.

- Run SQL Queries



