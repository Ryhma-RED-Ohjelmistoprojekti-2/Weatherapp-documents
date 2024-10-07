# Manual for Backend of Weatherapp.

## Table of Contents

- 1 Introduction
- 2 pom.xml


- S MySQL
    - S.1 Username & Password
        - S.2.2 Third sub-chapter

# 1 Introduction

This is manual for the whole backend of the application.
Manual consists tutorial and descriptions of each codes and solutions.

The backend was developed as a Java project with Spring Boot 
in Visual Studio Code environment. Therefore, we expect for reader 
to have some experience with Java and knowledge of Spring Boot.

We also used MySQL as the primary database. Therefore, the reader
must have MySQL installed in their host machine. In this manual,
we use MySQL from XAMPP Control Panel for introducing MySQL's connectivity
to application.

In chapter 2 - 4, we start presenting the essential files, that make and break the whole backend.

In chapter 5 - 8, we check files that are need for MVC.

# 2 pom.xml -file

A pom.xml -file is one of the most essential file in the backend.
It has all dependencies required to run Weatherapp, as shown in picture ##.

![Mysql_06_pom_xml](https://github.com/user-attachments/assets/65467e82-5b2a-4891-965e-5dc5edf3fd30)

Picture ##: pom.xml

Let's go step-by-step all dependencies.


	<dependency>

		<groupId>mysql</groupId>

		<artifactId>mysql-connector-java</artifactId>

		<version>8.0.33</version>

		<scope>runtime</scope>
	
	</dependency>

This is the dependency for MySQL database, a advice from GeeksForGeeks.
		
According to Co-pilot, this is a necessary plugin in modern
Java Maven projects, both locally and remote.

However, Maven require "sometimes" specific version of 
every depencies (I don't why it didn't require in
previous dependencies). Otherwise pom.xml will complain
about a missing built.

As 09 September 2024, latest version of mysql-connector-java
is 8.0.33 (built in April 18, 2023). Make sure it using current built

You can check latest built for the dependency from
https://mvnrepository.com/artifact/mysql/mysql-connector-java


# 3 application.properties -file

application.properties is essential a file for ...
as shown in picture ##.

Picture ##: application.properties.

Step-by-step explaination:

	spring.application.name=weatherapp

Line specifies name of our application.

---
	
	spring.datasource.url=jdbc:mysql:${DB_URL}

Line specifies the URL for our project's database,
which is called weatherDB.sql, in our MySQL server (locally).
DB_URL is given in a specific file.

//localhost:3306/weatherDB.sql

Note, that above line determines the **only** URL path of our database!

In order to import weatherDB.sql, we need a MySQL client 
(or CLI) that runs MySQL in background. For example,
start MySQL client via XAMPP control panel.

![Mysql_01_Run_apache_Mysql](https://github.com/user-attachments/assets/104595fa-8dd5-49ca-9b79-de35273b93ea)


See chapter S for more detailed explaination.

---

Next line is needed in order Java Application
access to a relational database, which is defined as Mysql
(see com.mysql). According to Co-pilot this establish connection.

	spring.datasource.driver-class-name=com.mysql.cj.jdbc.Driver

---

Need to add simple login system for the database.

	spring.datasource.username=${DB_USERNAME}
	spring.datasource.password=${DB_PASSWORD}

These are for login system of the database.

Each user must use their own username and password for the database,
that are made in MySQL server and saved in .env file. 

Since Github will ignore .env -file according to .gitignore -file,
we ensure that no sensitive information like username and password
will publicly published into Github. Hence, we have improved
data security for our database.

If you haven't created own username and password for the database,
see Chapter S tutorial for creating new username and password
in MySQL server, using XAMPP control panel.

---

	spring.jpa.hibernate.ddl-auto=update
	spring.jpa.show-sql=true

These configure hibernation of our database, 
i.e. will update and show weatherDB -database.

---
	spring.data.rest.base-path=/api

Determines REST path for database.

---

# S MySQL

## S.1 Username & password

In order to connect weatherDB -database from MySQL to Weatherapp (specifically backend),
then you must have your own username and password for the weatherDB database.

If you don't still have one, you need to create new one in MySQL.

In this step-by-step guide, we use XAMPP's MySQL as an example.


A) Open XAMPP Control Panel, e.g., from your Windows Start Menu.

![Mysql_00_Open_Xampp](https://github.com/user-attachments/assets/2045bb3f-1e19-4b4e-a5a9-88582a8c92e8)


B) Run MySQL and Appache in XAMPP Control Panel.

![Mysql_01_Run_apache_Mysql](https://github.com/user-attachments/assets/305c04fc-78a6-46d4-9119-4b7373663603)

C) Open Shell, which is on right side of XAMPP control panel. Login into Mysql with following command:

	mysql -u root -p
 
Press enter, if you haven't never changed your root's password.

![Mysql_05_mysql_shell](https://github.com/user-attachments/assets/afdb43c9-281a-427a-aadf-3aef9ea3a028)




D) 

Before you close, remember your user account privileges.

with command FLUSH PRIVILEGES;

Otherwise, your Mysql will forget all settings for your account,
therefore forgetting connection to database, 
making re-running the backend an awful headache (especially for me, Scrum master).

Also, from my experience, you can't insert same privileges after each running.
You have unfortunately always create new user account and password for each run.

So please, SAVE YOUR USER ACCOUNT PRIVILEGES FOR weatherdb.

### S.2.2 Third sub-chapters

Use if needed.
