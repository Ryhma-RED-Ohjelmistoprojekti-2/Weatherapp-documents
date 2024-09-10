This is manual on how we connect our application
to MySQL database.

# Chapter 1: Essential configurations in Java Spring Boot files

## 1.1 pom.xml -file

Make sure that pom.xml -file has state-to-art version
of following dependency:

**pom.xml**

<dependency>
 <groupId>mysql</groupId>
 <artifactId>mysql-connector-java</artifactId>
 <version>8.0.33</version>
 <scope>runtime</scope>
</dependency>


*Explaination*

Depency for MySQL database, a advice from GeeksForGeeks.
		
According to Co-pilot, this is a necessary plugin in modern
Java Maven projects, both locally and remote.

However, Maven require "sometimes" specific version of 
every depencies (I don't why it didn't require in
previous dependencies). Otherwise pom.xml will complain
about a missing built.

As 09 September 2024, latest version of mysql-connector-java
is 8.0.33 (built in April 18, 2023).

source: https://mvnrepository.com/artifact/mysql/mysql-connector-java



## 1.2 application.properties -file

Check application.properties -file has following lines.
All comments and explainations are marked with // -mark.


**application.properties**

// Specify name of our application

spring.application.name=weatherapp

---

// Configuration for MySQL Database 


// Next line specifies the URL for our created database
// which is called weatherDB.sql, in our MySQL server (locally).

spring.datasource.url=jdbc:mysql://localhost:3306/weatherDB.sql

// NOTE! Above line determines the only URL path of our database.
// In order to import weatherDB.sql, we need a MySQL client or CLI
// being runned.

---

// Next line is needed in order Java Application
// access to a relational database, which is defined as Mysql
// (see com.mysql). According to Co-pilot this establish connection.

spring.datasource.driver-class-name=com.mysql.cj.jdbc.Driver

---

// Need to add simple login system for case of security.

spring.datasource.username="REDryhma"
spring.datasource.password="saaAsema82024"

---

// Configuration for hibernation

spring.jpa.hibernate.ddl-auto=update
spring.jpa.show-sql=true

---

// Show database in the given REST path.

spring.data.rest.base-path=/api

---
---

// Used sources:

// https://spring.io/guides/gs/accessing-data-mysql

// https://dev.to/abhi9720/a-beginners-guide-to-crud-operations-of-rest-api-in-spring-boot-mysql-5hcl

// https://www.geeksforgeeks.org/spring-boot-crud-operations-using-mysql-database/

// https://www.geeksforgeeks.org/spring-boot-integration-with-mysql-as-a-maven-project/

// https://stackoverflow.com/questions/67260915/how-can-i-obtain-mysql-connector-java-maven-dependency

---
---

// Used prompts for Copilot:

// My MySQL database, called testMYQL.sql is locally located in same directory as the backend of Spring Boot Java. In many tutorials, they suggest to configure mysql database url as spring.datasource.url=jdbc:mysql://localhost:3306/your_database_name in the application.properties. Would it be sufficient enough, if I configure in application properties as spring.datasource.url=jdbc:mysql://localhost:3306/testMYQL.sql in order to import locally my testMYQL.sql, or did I missunderstood something?

// Is depedency of mysql-connector-java in pom.xml necessary anymore for state-of-art Spring Boot Java for connecting to Mysql database that is located locally?

// No matter how I trying add mysql-connector-java depency to pom.xml, Visual Studio Code warns following error "Project build error: 'dependencies.dependency.version' for mysql:mysql-connector-java:jar is missing.Java(0)". What does it mean?