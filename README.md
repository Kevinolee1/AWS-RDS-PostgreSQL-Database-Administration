# AWS-RDS-PostgreSQL-Database-Administration
Performed hands-on PostgreSQL administration on Amazon RDS, including database and table creation, SQL queries, user/role management, permissions, least-privilege access, and secure SSL database connectivity.

## Step 1 – Connect to the Amazon RDS PostgreSQL Instance

![PostgreSQL RDS Connection](images/01-postgresql-rds-connection.png)

**Figure 1 – Connecting to PostgreSQL on Amazon RDS:** I used the PostgreSQL `psql` command-line client from Windows PowerShell to establish a remote connection to the `cloud-dba-lab` Amazon RDS PostgreSQL instance.

The connection was established over **TLS 1.3**, providing encrypted communication between my local workstation and the RDS database server. After authentication, the `postgres=>` prompt confirmed that I had successfully connected to the PostgreSQL server and could begin performing database administration tasks.

## Step 2 – Verify the PostgreSQL Server Version

![PostgreSQL Server Version](https://github.com/Kevinolee1/AWS-RDS-PostgreSQL-Database-Administration/blob/7aee45684def112fc102efaef3e08e63c7e85b53/Screenshot%202026-10-05%20133640.png)

**Figure 2 – Verifying the PostgreSQL Server Version:** After connecting to the Amazon RDS PostgreSQL instance, I ran the `SELECT version();` command to verify the database engine and server version.

The query confirmed that the RDS instance was running **PostgreSQL 18.3 on a 64-bit Linux environment**. Verifying the server version helps confirm the database environment before performing administrative tasks and ensures compatibility with database features and management operations.

## Step 3 – Create and Verify the Application Database

![Create PostgreSQL Database](https://github.com/Kevinolee1/AWS-RDS-PostgreSQL-Database-Administration/blob/fb1cc3a2c7327152c3f7652ddbb655843d258024/Screenshot%202026-10-05%20133745.png)

**Figure 3 – Creating and Verifying the PostgreSQL Database:** I created a new PostgreSQL database named `companydb` using the `CREATE DATABASE` command.

After creating the database, I used the `\l` command to list the databases available on the Amazon RDS PostgreSQL instance. The results confirmed that `companydb` was successfully created with the `postgres` administrative user as the owner and UTF-8 encoding enabled.

This establishes a separate database environment for the application data and subsequent database administration tasks.

## Step 4 – Connect to the Company Database

![Connect to Company Database](images/04-connect-companydb.png)

**Figure 4 – Connecting to the Application Database:** I used the PostgreSQL `\c companydb` command to switch from the default `postgres` database to the newly created `companydb` database.

PostgreSQL confirmed the connection as the `postgres` administrative user. The session also shows that the connection is protected using **TLS 1.3 encryption**, securing communication between my local workstation and the Amazon RDS PostgreSQL instance.

The `companydb=>` prompt confirms that the database is active and ready for schema and table administration.

## Step 5 – Create the Employees Table

![Create Employees Table](images/05-create-employees-table.png)

**Figure 5 – Creating the Employees Table:** I created an `employees` table inside the `companydb` PostgreSQL database to store structured employee information.

The table includes an automatically generated `employee_id` primary key, required first and last name fields, department and job title fields, salary using a decimal data type, and a `hire_date` field that automatically defaults to the current date.

PostgreSQL returned `CREATE TABLE`, confirming that the table was successfully created in the Amazon RDS database.
