# Introduction

This is manual for the MySQL configurations for the backend.


# Chapter 0: Own MySQL -account and -password!
Everyone should first have their own account and password for the weatherDB database.

If you don't have one, you need to create new one in MySQL.

Our group used XAMPP control panel for running MySQL.

Bla bla bla

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

Used sources:

* https://spring.io/guides/gs/accessing-data-mysql

* https://dev.to/abhi9720/a-beginners-guide-to-crud-operations-of-rest-api-in-spring-boot-mysql-5hcl

* https://www.geeksforgeeks.org/spring-boot-crud-operations-using-mysql-database/

* https://www.geeksforgeeks.org/spring-boot-integration-with-mysql-as-a-maven-project/

* https://stackoverflow.com/questions/67260915/how-can-i-obtain-mysql-connector-java-maven-dependency

---
---

Used prompts for Copilot:

* My MySQL database, called testMYQL.sql is locally located in same directory as the backend of Spring Boot Java. In many tutorials, they suggest to configure mysql database url as spring.datasource.url=jdbc:mysql://localhost:3306/your_database_name in the application.properties. Would it be sufficient enough, if I configure in application properties as spring.datasource.url=jdbc:mysql://localhost:3306/testMYQL.sql in order to import locally my testMYQL.sql, or did I missunderstood something?

* Is depedency of mysql-connector-java in pom.xml necessary anymore for state-of-art Spring Boot Java for connecting to Mysql database that is located locally?

* No matter how I trying add mysql-connector-java depency to pom.xml, Visual Studio Code warns following error "Project build error: 'dependencies.dependency.version' for mysql:mysql-connector-java:jar is missing.Java(0)". What does it mean?