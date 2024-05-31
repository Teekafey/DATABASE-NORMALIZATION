![DATABASENORMALIZATION-ezgif com-video-to-gif-converter](https://github.com/Teekafey/DATABASE-NORMALIZATION/assets/169501567/3b6e2b91-c331-4ada-bc12-cdd2f1a0d4cb)
## What Is Database Normalization?
Simply, database normalisation is a process used for data modelling or database creation, where you organise your data and tables so it can be added and updated efficiently.

It can be done on any relational database, where data is stored in tables that are linked to each other. This means that normalization in a DBMS (Database Management System) can be done in Oracle, Microsoft SQL Server, MySQL, PostgreSQL and any other type of database.
For this project we would be using Oracle SQL Developer.

### But before we get into it...
#### Why do we normalize a database?
- To prevent the same data from being stored in more than one place (called an “insert anomaly”)
- To prevent updates being made to some data but not others (called an “update anomaly”)
- To prevent data not being deleted when it is supposed to be, or from data being lost when it is not supposed to be (called a “delete anomaly”)
- Essentially, to make the datbase more efficient, reducing storage space, ensuring queries run smoothly....to remove anomalies. (*You get it right?*)

### There are six(6) forms of Normalization

- First Normal Form (1NF)
- Second Normal Form (2NF)
- Third Normal Form (3NF)
- Boyce-Codd Normal Form (BCNF)
- Fourth Normal Form (4NF)
- Fifth Normal Form (5NF)

#### But for this project we would be going up till the Third Normal Form (3NF). It is the most commonly used.

### Okay, now let's get to the good stuff...
We'll be using a **customer orders table** for this project.
Here is a snippet of what we are working with; [**pg1**](https://github.com/Teekafey/DATABASE-NORMALIZATION/blob/main/DN_files/Cust_orders%201.jpg), [**pg2**](https://github.com/Teekafey/DATABASE-NORMALIZATION/blob/main/DN_files/Cust_orders%202.jpg)


## [First Normal Form (1NF)](https://github.com/Teekafey/DATABASE-NORMALIZATION/blob/main/First%20Normal%20Form.md)

## [Second Normal Form(2NF)](https://github.com/Teekafey/DATABASE-NORMALIZATION/blob/main/Second%20Normal%20Form.md)

## [Third Normal Form(3NF)](https://github.com/Teekafey/DATABASE-NORMALIZATION/blob/main/Third%20Normal%20Form.md)

