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

> Nationality: No, and here's why. The nationality doesn’t describe what a customer is, and isn’t dependent on a customer.

What does that mean for this database?

I would suggest creating a separate table for nationality, and relating them to a customer

The [Nationality](https://github.com/Teekafey/DATABASE-NORMALIZATION/blob/main/DN_files/nationality.jpg) Table (values inserted)
```SQL
CREATE TABLE nationality (
  Nationality_CODE VARCHAR(5) 
  Nationality VARCHAR2(50) NOT NULL UNIQUE -- Nationality name (unique to prevent duplicates)
);
```
Relating it to the Customers Table
```SQL
ALTER TABLE customers
ADD Nationality_CODE VARCHAR(5) REFERENCES nationality(Nationality_CODE);
```

The New Customer's Table
![cust](https://github.com/Teekafey/DATABASE-NORMALIZATION/assets/169501567/b1374f6b-da85-4992-b101-00f6f491a11b)

3. The [Orders](https://github.com/Teekafey/DATABASE-NORMALIZATION/blob/main/DN_files/orders.jpg)
- Are each of these fields dependent on the Order_ID value?
> Customer_ID - Yes, this tells us whch Customer owns which Order.
  
> Order_Date - Yes, this describes the date an order was made.

> Order_Shipment_Date -  Yes, this describes the date an order was shipped.

> Order_Received_Date -  Yes, this describes the date an order was received.

The rest of the columns do not exactly describe the order_id, why is this:

> In the Purchase_Touchpoint column, we can see that users ordered through Phone(app) and Laptop(web appp). The following columns: Order_Salesman, Shipment_Charge, Transaction_Status, Purchase_Touchpoint, Purchase_Freq.

We can create a Transaction Details table that will tell us who will process our order/transaction (Order_Salesman), the Shipment_Charge, the Transaction_Status, where a customer ordered from (Purchase_Touchpoint).



