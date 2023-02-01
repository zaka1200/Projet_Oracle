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
  mark number(10) NOT NULL
);
```
