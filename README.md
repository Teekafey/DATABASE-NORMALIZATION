# DATABASE-NORMALIZATION
## What Is Database Normalization?
Simply, database normalisation is a process used for data modelling or database creation, where you organise your data and tables so it can be added and updated efficiently.

It can be done on any relational database, where data is stored in tables that are linked to each other. This means that normalization in a DBMS (Database Management System) can be done in Oracle, Microsoft SQL Server, MySQL, PostgreSQL and any other type of database.
For this project I will be using Oracle SQL Developer

### But before we get into it...
#### Why do we normaalize a database?
- To prevent the same data from being stored in more than one place (called an “insert anomaly”)
- To prevent updates being made to some data but not others (called an “update anomaly”)
- To prevent data not being deleted when it is supposed to be, or from data being lost when it is not supposed to be (called a “delete anomaly”)
- Essentially, to make the datbase more efficient, reducing storage space, ensuring queries run smoothly....to remove anomalies. (*You get it right?*)


### Okay, now let's get to the good stuff..
We'll be using a **customer orders table** for this project.
Here is a snippet of what we are working with..[pg1](https://github.com/Teekafey/DATABASE-NORMALIZATION/blob/main/DN_files/Cust_orders%201.jpg),[pg2]([https://github.com/Teekafey/DATABASE-NORMALIZATION/blob/main/1dn.jpg](https://github.com/Teekafey/DATABASE-NORMALIZATION/blob/main/DN_files/Cust_orders%202.jpg))


#### <u>First Normal Form (1NF)</u>
- Each set of columns must uniquely identify a row. Does the combination of all columns make a unique row every single time?
- What field can be used to uniquely identify the row?
  
If the table can answer these two questions, then it is in 1NF


#### But does it?

No.
There could be the same combination of data, and it would represent a different row.

We can se here that this table has;
- Customers details (Customer_ID, First Name,	Last Name,	Gender, Email Address, Phone Number, Age, Nationality),
- Their Address details (Address, City, State, Postal Code, Country),
- Their order details (Order_ID,	Order Date,	Order Received Date,	Order Shipment Date, Order Salesman, Shipment Charge, Transaction_Type	Purchase Touchpoint,	Purchase status).


The table violates 1NF because a single customer can have multiple entries for their orders. This redundancy can lead to data inconsistency and make it difficult to manage customer and order information efficiently.

We would separate this table into Customers, Address and Orders table.

Orders Table (values inserted)
```SQL
CREATE TABLE orders (
  Order_ID NUMBER PRIMARY KEY, -- Unique identifier for each order
  Customer_ID NUMBER NOT NULL, -- Foreign key referencing the customers table (assuming a one-to-many relationship
  FOREIGN KEY (Customer_ID) REFERENCES customers(Customer_ID), -- Enforces relationship
  Order_Date DATE NOT NULL, -- Date the order was placed
  Order_Received_Date DATE, -- Date the order was received 
  Order_Shipment_Date DATE, -- Date the order was shipped 
  Order_Salesman VARCHAR2(50), -- Name of the salesperson who handled the order 
  Shipment_Charge NUMBER, -- Shipment charge associated with the order 
  Transaction_Status VARCHAR2(20), -- Status of transaction (e.g., complete, cancelled) --Chagned from Transaction_Type
  Purchase_Touchpoint VARCHAR2(50), -- Where the purchase was initiated (e.g phone(app) or desktop(web app))
  Purchase_Freq VARCHAR2(20) -- How frequent orders are made from a customer --Changed from Purchase_Status
);
```
Customers Table (values inserted)
```SQL
CREATE TABLE customers (
  Customer_ID NUMBER PRIMARY KEY, -- Unique identifier for each customer 
  First_Name VARCHAR2(50) NOT NULL, -- Customer's first name 
  Last_Name VARCHAR2(50) NOT NULL, -- Customer's last name 
  Gender VARCHAR2(10), -- Customer's gender 
  Email_Address VARCHAR2(255) UNIQUE, -- Customer's email address 
  Phone_Number VARCHAR2(20), -- Customer's phone number 
  Age NUMBER, -- Customer's age
  Nationality VARCHAR2(50) -- Customer's nationality 
);
```

Address Table (values inserted)
```SQL
CREATE TABLE address (
  Customer_ID NUMBER PRIMARY KEY, -- Foreign key referencing the customers table (assuming a one-to-one relationship)
  FOREIGN KEY (Customer_ID) REFERENCES customers(Customer_ID), -- Enforces relationship
  Address VARCHAR2(100) NOT NULL, -- FCustomer's Address
  City VARCHAR2(50) NOT NULL, -- City name
  State VARCHAR2(50) NOT NULL, -- State or province name
  Postal_Code VARCHAR2(20), -- Postal code or ZIP code
  Country VARCHAR2(50) NOT NULL -- Country name
);
```


