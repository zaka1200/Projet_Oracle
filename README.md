# Projet_Oracle

# Concept

In summary, the goal of this project is to provide a secure web platform with a variety of user profiles. The platform should be created using the programming language of your choice and connected to an Oracle data base. There will be two users in the database: an administrator with full access rights and a regular user with access limits. To ensure that the access limits are followed, the users' connections will be tested. To record the acts taken by each user, journalization files will finally be generated.

# Introduction

This platform is an educational management system that displays the notes of students. This system provides administrators with a friendly interface for managing student information such as name, notes, and subjects. The use of multiple user profiles ensures secure access. A data administrator (prof) has access to all of the data and has the ability to modify it. The students themselves can only view their personal information without having the option to change it.

Our goal is to provide a secure web platform with a straightforward connection that includes a connection button and two text fields for the user's name and password. The platform will be linked to an Oracle data base.

After that we are going to get a web page that contains the list of marks and subjects of the user and if its the admin it gives him the right to modify the marks

We'll test the access to our platform by concurrently connecting the two users using Node.js to make sure that the connection adheres to the proper access rights for the type of user. we are going to use thunder client to test the requests before testing our web platform.

# Oracle :

Oracle is a popular relational database management system (RDBMS) used for managing and storing large amounts of structured data. It offers advanced features such as security, reliability, scalability, and data recovery, making it a popular choice for businesses and organizations. Oracle is known for its flexible architecture, allowing it to run on multiple operating systems and providing compatibility with different programming languages.

> after setting up oracle sata base management in our local machine we move to create the tables and the users

## Tables creation :  

### **users Table**
In this project, a data base that was created with system users will be used as the basis for work.
creation of the "student" table with the three columns "student id," "name," and "email." The primary key column "student id" is defined as primary key it can not be null

```sql
CREATE TABLE student (
  student_id PRIMARY KEY,
  name varchar(30) NOT NULL,
  email varchar(30) NOT NULL
);
```
### **users Table**

the creation of the "notes" table with the four columns "note id," "student id," "subject," and "grade."
In reference to the column "student id" of table "student," column "note id" is defined as the primary key, and column "student id" is defined as the foreign key.

```sql
CREATE TABLE notes (
  note_id number(10) PRIMARY KEY,
  student_id number(10) NOT NULL,
  FOREIGN KEY (student_id) REFERENCES student(student_id)
  subject varchar(30) NOT NULL,
  grade number(10) NOT NULL
);
```
## Users creation :

Here we have to create two users a simple user and an adminstrator ,to create them we are going to follow these steps :

- we have to connect to the Oracle database as a user with sufficient privileges to create new users, such as the SYSTEM user. wich is already done.
- we run the following SQL command to create a new user:
```sql
CREATE USER user1 IDENTIFIED BY user1 default tablespace users;
CREATE USER admin IDENTIFIED BY admin default tablespace users;
```
- now we need to grant the necessary privileges to these users, For example, to grant the CREATE SESSION privilege

## Grant privileges :

we need to allow "admin" user access to all privileges.

```sql
grant all  privileges to admin;
```
Granting the user "user1" access to the "new session" and "select" functions on the "student" and "notes" database.
```sql
GRANT CREATE SESSION TO user1;
GRANT SELECT ON student TO user1;
GRANT SELECT ON notes TO user1;
```
## Testing :

for the fisrt test we are going to use our simple user "user1" 
to do that we are goin to run a simple SQL query such as :
```sql
INSERT INTO notes (note_id,student_id,subject,grade)
VALUES (1, 1, "oracle",19);
```
we obtain an error because we didnt give the user "user1" the privilege to insert any value in notes table

![image](https://user-images.githubusercontent.com/121964432/216113198-3f87909c-6c1d-4fe4-96ec-104ffa68d9fc.png)

now we are going to do the same process but with admin privileges

```sql
INSERT INTO notes (note_id,student_id,subject,grade)
VALUES (1, 1, "oracle",19);
```
as you can see we were able to insert a value in the notes table

![admin ana](https://user-images.githubusercontent.com/121964432/216117065-a5c63225-9ae2-4263-b0cb-a2634563dc4e.png)

This is a simple example, using "admin" as an admin and "user1" as a normal user, you can perform various privileges on other types of users.


# WEB Platform test :

![shema](https://user-images.githubusercontent.com/121964432/216121058-1975847b-de10-429d-a6bc-056f34f75439.png)

Here are the general steps for connecting from the platform to the data base:
- Configuring the connection parameters: This includes specifying the connection details, which includes the user name and password.
Charge the Oracle driver for the client platform: The Oracle Connection Pilote is a library that enables one to connect to the Oracle Database, often known as Oracledb for Node. js
- Establishing a connection The client platform can establish a secure connection with the Oracle data base by using the connection information and the Oracle pilot, according on the entered profile.
- Execute queries: After establishing a connection, the client platform can run SQL queries to interact with the data stored in the Oracle database.
- Terminate the connection: Terminating the connection will free up the platform's used resources when it is no longer necessary for it to connect to the database.

## Overview

Our code is an example of a server-side Web application that implements login and note-display functionality.
- An authentication form where the user can enter their user id and password is displayed when they access the home page using the HTTP GET method. User submission of the form triggers the HTTP POST / login method to be used. This method compares the user's identity information with the list of authorized users by extracting it from the body of the request. A notice of login failure is sent if the user cannot be found in the list. Otherwise, the connection is recorded in a journal file, and the user is directed to the appropriate page according to his or her user name.
- A group of SQL queries are executed on an Oracle database when a user accesses a web page using the HTTP GET method. Each query's result is converted to HTML for a table display on the page.

##  Web platfrorm test:

The code checks to see if the connection information corresponds to one of the authorized users when the user logs in by entering their username and password in a form on the home page. If the information is accurate, the user will be directed to a page appropriate for their user type (admin or normal). Additionally, the code records the connection's time in a journal file.

![user1](https://user-images.githubusercontent.com/121964432/216136553-9af9f889-f89c-4c4f-8c41-34c877bf35b3.png)

if the user is a normal useer like user1 he can only view the table of marks :

![user1 table](https://user-images.githubusercontent.com/121964432/216137410-3d1727f1-9061-4ab1-8efe-cbe4ce6a43b2.png)

If the user is an administrator, they can view a page displaying the database's table of marks and he can modify on it. The code uses the OracleDB library to run some SQL queries to modify the data in this table and generate an HTML table for each result.
Here is an example of a connection with admin:

![admin](https://user-images.githubusercontent.com/121964432/216137809-f5b6bdcd-c619-4216-b5a9-872c75e51c8c.png)

- first we are going to login as an administrator using the id  "admin" and the password "admin" :

![step1](https://user-images.githubusercontent.com/121964432/216138248-0a489a02-0231-47ef-b2fa-de6617cacdbc.png)

- as you can see we got a web page containing the table in addition of a button and an input to modify the mark

![step2](https://user-images.githubusercontent.com/121964432/216138526-1658b7f9-a5b4-4797-ac2d-b6e699a274c1.png)

- Here we change the mark to 20

![step3](https://user-images.githubusercontent.com/121964432/216138551-7d85cda1-807d-4518-9553-2cdcb72850fe.png)

- after clicking "modify" button we can see the table is updated
