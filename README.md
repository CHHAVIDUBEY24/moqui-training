Moqui Framework – MySQL Database Configuration
Overview

The purpose of this assignment is to configure the Moqui Framework to use a MySQL database for application development.
This setup includes installing and securing MySQL, configuring database connectivity in Moqui, loading initial data using Gradle, and verifying the setup through the Moqui System Dashboard.

Prerequisites:

Java JDK 11 or higher

Git

MySQL Server (version 8.0.32 or higher)

MySQL Workbench (optional but recommended)

Moqui Framework source code


Step 1: Install and Secure MySQL
1. MySQL Installation

Installed MySQL Community Server 8.0.32

Set a strong root password during installation

2. Secure MySQL Installation

The following command was executed to secure MySQL:

mysql_secure_installation


During this process:

Root password was set

Anonymous users were removed

Remote root login was disabled

Test database was removed

Privilege tables were reloaded

This ensured the MySQL installation was secure.

Step 2: Add MySQL JDBC Driver

A JDBC driver allows Java-based applications (like Moqui) to communicate with a database.

Steps Followed:

Downloaded MySQL Connector/J 8.0.32

Copied the JDBC .jar file to the following directory:

moqui-framework/runtime/lib

Step 3: Create Database and User
1. Login to MySQL
mysql -u root -p

2. Create Database with UTF-8 Charset
CREATE DATABASE moqui CHARACTER SET utf8;
UTF-8 is used to support multiple languages and Unicode characters.

3. Create Database User
CREATE USER 'moqui'@'localhost' IDENTIFIED BY '@12345abC';

4. Grant Permissions
GRANT ALL PRIVILEGES ON moqui.* TO 'moqui'@'localhost';
FLUSH PRIVILEGES;

Step 4: Update Moqui Configuration
Configuration File
moqui-framework/runtime/conf/MoquiDevConf.xml

Database Configuration Added
<default-property name="entity_ds_db_conf" value="mysql8"/>
<default-property name="entity_ds_host" value="127.0.0.1"/>
<default-property name="entity_ds_port" value="3306"/>
<default-property name="entity_ds_database" value="moqui"/>
<default-property name="entity_ds_user" value="moqui"/>
<default-property name="entity_ds_password" value="@12345abC"/>

Explanation:

entity_ds_db_conf specifies the MySQL version configuration

entity_ds_host defines the database host (local machine)

127.0.0.1 refers to the local system

Other properties define database name and credentials

Step 5: Load Data Using Gradle
Navigate to Moqui Directory
cd moqui-framework

Load Initial Data
./gradlew load




Step 6: Verify Setup

Open the following URL in a browser:

http://localhost:8080/vapps/system/dashboard


If the System Dashboard loads correctly, the configuration is successful.

Additional Concepts Explained
CHARACTER SET utf8

Supports international characters and Unicode


IP Address and Host Details

Laptop IP Address: Can be checked using ipconfig (Windows)

entity_ds_host: Specifies where the database server is running

Conclusion

Through this assignment, MySQL was successfully installed, secured, and integrated with the Moqui Framework.
The database connection was verified by loading data and accessing the Moqui System Dashboard.