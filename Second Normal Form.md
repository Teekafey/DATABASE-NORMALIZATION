## Second Normal Form(2NF)
How do we get a Database to be in Second Normal Form?

- The tables should be in First Normal Form.
- All of the non-key attributes are dependent on the primary key. Are all of the columns in each table dependent on and specific to the primary key?

We have fufilled the first attribute of the First Normal Form. 

So let's go to the second...

1. The [Address](https://github.com/Teekafey/DATABASE-NORMALIZATION/blob/main/DN_files/address.jpg) Table
  
- Are each of these fields dependent on the Customer_Id value?
> Address: Yes, and this column helps to describe where the user lives (house number and street).

> City: Yes, and this column helps to describe what city the user lives.

> State: Yes, and this column helps to describe what state the user lives.

> Postal Code: Yes, and this column helps to describe the code of the city the user lives.

> Country: Yes, and this column helps to describe what country the user lives.

2. The [Customers](https://github.com/Teekafey/DATABASE-NORMALIZATION/blob/main/DN_files/customers.jpg) Table

- Are each of these fields dependent on the Customer_Id value?
> First Name: Yes, and this column helpps to describe the first_name of the user.

> Last Name: Yes, and this column helps to describe the last_name of the user.

> Gender: Yes, and this column helps to describe the gender of the user.

> Email Address: Yes, and this column helps to describe the email of the user.

> Phone Number: Yes, and this column helps to describe the contact number of the user.

> Age: Yes, and this column helps to describe the age of the user.

> Nationality: Yes, it is. (We already get it).

3. The [Orders](https://github.com/Teekafey/DATABASE-NORMALIZATION/blob/main/DN_files/orders.jpg) Table
- Are each of these fields dependent on the Order_ID value?
> Customer_ID - Yes, this tells us whch Customer owns which Order.
  
> Order_Date - Yes, this describes the date an order was made.

> Order_Shipment_Date -  Yes, this describes the date an order was shipped.

> Order_Received_Date -  Yes, this describes the date an order was received.

The rest of the columns do not exactly describe the Order_id, why is this:

> In the Orders table, 'Order_Salesman', 'Transaction_Type', 'Purchase_Touchpoint', 'Shipment_Charge' , and 'Purchase_Status' are still present. There could be different Salesmen, Shipment Charge, Touchpoint or Status for different Orders.

We need to further normalize by separating these into distinct tables.

We can create a Order Salesman and a Transaction Details table that will tell us who will process our order/transaction (Order_Salesman), the Shipment_Charge, the Transaction_Status, where a customer ordered from (Purchase_Touchpoint).

The [Salesman](https://github.com/Teekafey/DATABASE-NORMALIZATION/blob/main/DN_files/SALES.jpg) Table
```SQL
CREATE TABLE order_salesmen (
  Order_ID NUMBER,
  Salesman_ID NUMBER,
  CONSTRAINT order_salesmen_pk PRIMARY KEY (Order_ID, Salesman_ID),
  CONSTRAINT order_salesmen_fk_order FOREIGN KEY (Order_ID) REFERENCES orders(Order_ID),
  CONSTRAINT order_salesmen_fk_salesman FOREIGN KEY (Salesman_ID) REFERENCES salesmen(Salesman_ID)
);

CREATE TABLE salesmen (
  Salesman_ID NUMBER PRIMARY KEY, -- Unique identifier for each salesman
  Salesman_Name VARCHAR2(100) NOT NULL -- Salesman's name
);

```
The [Transactions](https://github.com/Teekafey/DATABASE-NORMALIZATION/blob/main/DN_files/TRANSACT.jpg) Table
```SQL
CREATE TABLE transactions (
  Transaction_ID NUMBER PRIMARY KEY, -- Unique identifier for each transaction
  Order_ID NUMBER NOT NULL, -- Foreign key referencing the orders table
  Transaction_Type VARCHAR2(100), -- Type of transaction (e.g., Credit Card, PayPal)
  Purchase_Touchpoint VARCHAR2(100), -- Point of purchase (e.g., Web, Phone)
  Purchase_Status VARCHAR2(100), -- Status of purchase (e.g., Completed, Pending)
  Shipment_Charge NUMBER, -- Charge for shipping the order
  FOREIGN KEY (Order_ID) REFERENCES orders(Order_ID), -- Enforces relationship
  CONSTRAINT unique_order_transaction UNIQUE (Order_ID, Transaction_ID) -- Ensures unique combination
);
```
### Our Database is in Second Normal Form

