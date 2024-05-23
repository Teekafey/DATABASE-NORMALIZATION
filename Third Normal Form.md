## Third Normal Form (3NF)

Third normal form is the final stage of the most common normalization process. The rule for this is:

- Fulfils the requirements of Second Normal Form
- Has no transitive functional dependency

A transitive functional dependency exists when a non-key attribute depends on another non-key attribute, which in turn depends on the primary key.

It means that every attribute that is not the primary key must depend on the primary key and the primary key only.


We have fufilled the first attribute of the Second Normal Form. 

So let's go to the third...

If we take a closer look at our  [Second Normalization Form](https://github.com/Teekafey/DATABASE-NORMALIZATION/blob/main/Second%20Normal%20Form.md), we can see that the table _**even**_ meets our Third normal form requirement as all attributes depend on their respective primary key.

Here are the final database tables;
- #### [Customers](https://github.com/Teekafey/DATABASE-NORMALIZATION/blob/main/DN_files/customers.jpg)
- #### [Address](https://github.com/Teekafey/DATABASE-NORMALIZATION/blob/main/DN_files/address.jpg)
- #### [Orders](https://github.com/Teekafey/DATABASE-NORMALIZATION/blob/main/DN_files/Orders%20new.jpg)
- #### [Salesman](https://github.com/Teekafey/DATABASE-NORMALIZATION/blob/main/DN_files/SALES.jpg)
- #### [Transaction](https://github.com/Teekafey/DATABASE-NORMALIZATION/blob/main/DN_files/TRANSACT.jpg)

This is what our Database may look like;
![cust model](https://github.com/Teekafey/DATABASE-NORMALIZATION/assets/169501567/9cba53f8-3c46-413f-9b48-277013fef907)


# _THANK YOU!_
