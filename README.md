# AWS-RDS-PostgreSQL-Database-Administration
Performed hands-on PostgreSQL administration on Amazon RDS, including database and table creation, SQL queries, user/role management, permissions, least-privilege access, and secure SSL database connectivity.

## Step 1 – Connect to the Amazon RDS PostgreSQL Instance

![PostgreSQL RDS Connection](https://github.com/Kevinolee1/AWS-RDS-PostgreSQL-Database-Administration/blob/8aac45d2213e16363e9e64f5fbba62dd17534488/Screenshot%202026-10-06%20064203.png)

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

![Connect to Company Database](https://github.com/Kevinolee1/AWS-RDS-PostgreSQL-Database-Administration/blob/a93c28df33bd39675980d7fac1db469d2babe63c/Screenshot%202026-10-05%20133828.png)

**Figure 4 – Connecting to the Application Database:** I used the PostgreSQL `\c companydb` command to switch from the default `postgres` database to the newly created `companydb` database.

PostgreSQL confirmed the connection as the `postgres` administrative user. The session also shows that the connection is protected using **TLS 1.3 encryption**, securing communication between my local workstation and the Amazon RDS PostgreSQL instance.

The `companydb=>` prompt confirms that the database is active and ready for schema and table administration.

## Step 5 – Create the Employees Table

![Create Employees Table](https://github.com/Kevinolee1/AWS-RDS-PostgreSQL-Database-Administration/blob/a517f4e6cf8480d8cd90b94d021767d22f8e9ca0/Screenshot%202026-10-05%20133946.png)

**Figure 5 – Creating the Employees Table:** I created an `employees` table inside the `companydb` PostgreSQL database to store structured employee information.

The table includes an automatically generated `employee_id` primary key, required first and last name fields, department and job title fields, salary using a decimal data type, and a `hire_date` field that automatically defaults to the current date.

PostgreSQL returned `CREATE TABLE`, confirming that the table was successfully created in the Amazon RDS database.

## Step 6 – Verify the Employees Table

![Verify Employees Table](https://github.com/Kevinolee1/AWS-RDS-PostgreSQL-Database-Administration/blob/a4e4aac69750c452ee373152749663d39c85e14b/Screenshot%202026-10-05%20134037.png)

**Figure 6 – Verifying the Employees Table:** After creating the `employees` table, I used the PostgreSQL `\dt` command to list the tables within the `companydb` database.

The results confirmed that the `employees` table was successfully created in the `public` schema and is owned by the `postgres` administrative user. This verification ensured that the table was available before continuing with additional schema and data administration tasks.

## Step 7 – Inspect the Employees Table Schema

![Employees Table Schema](images/07-employees-table-schema.png)

**Figure 7 – Inspecting the Employees Table Structure:** I used the PostgreSQL `\d employees` command to inspect the structure of the `employees` table.

The output verified the configured columns and data types, including integer, variable-length character, numeric, and date fields. It also confirmed the `NOT NULL` constraints on required employee information, the `CURRENT_DATE` default for `hire_date`, and the primary key index on `employee_id`.

This verification confirmed that the table schema and constraints were configured correctly before inserting employee records.

## Step 8 – Insert Employee Records

![Insert Employee Records](images/08-insert-employee-records.png)

**Figure 8 – Populating the Employees Table:** I used an SQL `INSERT INTO` statement to add five sample employee records to the `employees` table.

The records represent multiple departments and job roles with corresponding salary information. PostgreSQL returned `INSERT 0 5`, confirming that all five records were successfully inserted into the Amazon RDS PostgreSQL database.

This populated the table with sample data that could be used for querying and additional database administration tasks.

## Step 9 – Query and Verify Employee Records

![Query Employee Records](images/09-query-employee-records.png)

**Figure 9 – Querying Employee Data:** I used the SQL `SELECT * FROM employees;` statement to retrieve all records stored in the `employees` table.

The query returned all five employee records with their employee IDs, names, departments, job titles, salaries, and hire dates. This confirmed that the previous `INSERT` operation successfully stored the records and that the data could be retrieved from the Amazon RDS PostgreSQL database.

The automatically generated employee IDs and hire dates also confirmed that the primary key sequence and `CURRENT_DATE` default were functioning as configured.

## Step 10 – Create a PostgreSQL Login Role

![Create Reporting User](images/10-create-reporting-user.png)

**Figure 10 – Creating a Database Login Role:** I created a PostgreSQL role named `reporting_user` with login capability to establish a separate database account for reporting access.

Rather than using the administrative `postgres` account for routine database access, the new role provides a dedicated identity that can be assigned only the permissions required for its function.

The password has been redacted from the screenshot to prevent credentials from being exposed in the public repository.

