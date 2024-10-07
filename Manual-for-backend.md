# Manual for Backend of Weatherapp.

## Table of Contents

- 1 Introduction



- 2 MySQL
    - 2.1 Username & Password
        - 2.2.2 Third sub-chapter

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

# - MySQL

## -.1 Username & password

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

# Chapter 1: Essential configurations in Java Spring Boot files

## 1.1 pom.xml -file

Make sure that pom.xml -file has state-to-art version
of following dependency:





	#pom.xml

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
is 8.0.33 (built in April 18, 2023).

You can check latest built for dependency
from https://mvnrepository.com/artifact/mysql/mysql-connector-java


## 1.2 application.properties -file

Check application.properties -file has following lines.


	#application.properties

	#Specifying name of our application

	spring.application.name=weatherapp

---

Next line specifies the URL for our created database
which is called weatherDB.sql, in our MySQL server (locally).

	#Configuration for MySQL Database 
	
	spring.datasource.url=jdbc:mysql:${DB_URL}

DB_URL is given in a specific file.

//localhost:3306/weatherDB.sql

NOTE! Above line determines the **only** URL path of our database.

In order to import weatherDB.sql, we need either a MySQL client 
or CLI, that runs MySQL in background.

---

Next line is needed in order Java Application
access to a relational database, which is defined as Mysql
(see com.mysql). According to Co-pilot this establish connection.

	spring.datasource.driver-class-name=com.mysql.cj.jdbc.Driver

---

Need to add simple login system for the database.

	spring.datasource.username=${DB_USERNAME}
	spring.datasource.password=${DB_PASSWORD}

Everyone in group has their own username and password for the database.

---

We have to also configure hibernation.

	// Configuration for hibernation

	spring.jpa.hibernate.ddl-auto=update
	spring.jpa.show-sql=true

---

Lastly we determine REST path for database.

	// Show database in the given REST path.

	spring.data.rest.base-path=/api

---
---
