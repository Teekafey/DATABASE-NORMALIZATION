## First Normal Form (1NF)
For a Database to be in First Normal Form:
- Each set of columns must uniquely identify a row. Does the combination of all columns make a unique row every single time?
- What field can be used to uniquely identify the row?
  
If the table can answer these two questions, then it is in 1NF.



#### But does it?

No.
There could be the same combination of data, and it would represent a different row.

We need to nemove repeating groups and create separate tables for related data to achieve the First Normal Form (1NF).

We can see in [**pg1**](https://github.com/Teekafey/DATABASE-NORMALIZATION/blob/main/DN_files/Cust_orders%201.jpg),[**pg2**](https://github.com/Teekafey/DATABASE-NORMALIZATION/blob/main/DN_files/Cust_orders%202.jpg) that this table has;
- Customers details (Customer_ID, First Name,	Last Name,	Gender, Email Address, Phone Number, Age, Nationality),
- Their Address details (Address, City, State, Postal Code, Country),
- Their order details (Order_ID,	Order Date,	Order Received Date,	Order Shipment Date, Order Salesman, Shipment Charge, Transaction_Type	Purchase Touchpoint,	Purchase status).


The table violates 1NF because a single customer can have multiple entries for their orders. This redundancy can lead to data inconsistency and make it difficult to manage customer and order information efficiently.


We would separate this table into Customers, Address and Orders table.
Each set of columns must uniquely identify a row.

[Orders Table](https://github.com/Teekafey/DATABASE-NORMALIZATION/blob/main/DN_files/orders.jpg) (values inserted)
```SQL
CREATE TABLE orders (
  Order_ID NUMBER PRIMARY KEY, -- Unique identifier for each order
  Customer_ID NUMBER NOT NULL, -- Foreign key referencing the customers table (assuming a one-to-many relationship
  FOREIGN KEY (Customer_ID) REFERENCES customers(Customer_ID), -- Enforces relationship
  Order_Date DATE NOT NULL, -- Date the order was placed
  Order_Shipment_Date DATE, -- Date the order was shipped 
  Order_Received_Date DATE, -- Date the order was received 
  Order_Salesman VARCHAR2(50), -- Name of the salesperson who handled the order 
  Shipment_Charge NUMBER, -- Shipment charge associated with the order 
  Transaction_Status VARCHAR2(20), -- Status of transaction (e.g., complete, cancelled) --Chagned from Transaction_Type
  Purchase_Touchpoint VARCHAR2(50), -- Where the purchase was initiated (e.g phone(app) or desktop(web app))
  Purchase_Freq VARCHAR2(20) -- How frequent orders are made from a customer --Changed from Purchase_Status
);
```
[Customers Table](https://github.com/Teekafey/DATABASE-NORMALIZATION/blob/main/DN_files/customers.jpg) (values inserted)
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

[Address Table](https://github.com/Teekafey/DATABASE-NORMALIZATION/blob/main/DN_files/address.jpg) (values inserted)
```SQL
CREATE TABLE address (
  Customer_ID NUMBER PRIMARY KEY, -- Foreign key referencing the customers table (assuming a one-to-one relationship)
  FOREIGN KEY (Customer_ID) REFERENCES customers(Customer_ID), -- Enforces relationship
  Address VARCHAR2(100) NOT NULL, -- Customer's Address
  City VARCHAR2(50) NOT NULL, -- City name
  State VARCHAR2(50) NOT NULL, -- State or province name
  Postal_Code VARCHAR2(20), -- Postal code or ZIP code
  Country VARCHAR2(50) NOT NULL -- Country name
);
```
### Our Database is in First Normal Form
