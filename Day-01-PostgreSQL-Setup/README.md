# Day 1 – PostgreSQL Database Setup and SQL Fundamentals

## Project Overview

This lab focuses on setting up PostgreSQL on Ubuntu Linux and creating a sample security monitoring database.

The objective was to understand database creation, table design, data insertion, and SQL queries using a simulated cloud security environment.

## Environment

- Operating System: Ubuntu Linux
- Virtualisation: Oracle VirtualBox
- Database: PostgreSQL 17
- Interface: PostgreSQL Command Line (psql)
- Database Name: `security_lab`

## Tasks Completed

### 1. PostgreSQL Setup
- Accessed PostgreSQL through the Linux terminal.
- Logged in using the PostgreSQL administrative account.
- Connected to the PostgreSQL command-line interface.

### 2. Database Creation

Created a database named `security_lab`.

```
CREATE DATABASE security_lab;
```

### 3. Table Creation

Created three tables to simulate a basic security monitoring environment.

**Users Table**
- id
- username
- email
- created_at

**Events Table**
- id
- user_id
- event_type
- ts

**Authentication Logs Table**
- id
- ip
- status
- ts

### 4. Data Insertion

Inserted sample records into the three tables.

The sample data represents:
- User account information
- Login events
- File upload activities
- Password change activities
- Successful and failed authentication attempts

### 5. SQL Query Execution

Executed SELECT queries to retrieve and verify the inserted records.

```
SELECT * FROM users;

SELECT * FROM events;

SELECT * FROM auth_logs;
```

Verified that the records were successfully inserted and retrieved.

## Security Relevance

This database provides a foundation for understanding security monitoring and database analysis.

The authentication log data can later be used to investigate:

- Failed login attempts
- Successful authentication events
- Suspicious IP addresses
- User activity patterns
- Potential unauthorised access

## Screenshots

| Screenshot | Description |
|---|---|
| 01-database-and-table-creation.png | Database and table creation |
| 02-data-insertion-and-verification.png | Inserting sample records |
| 03-select-query-results.png | Retrieving and verifying records |

## Key Learning Outcomes

- PostgreSQL installation and access
- Database creation and management
- Relational table creation
- Understanding primary and foreign keys
- Inserting records using SQL
- Retrieving records using SELECT queries
- Understanding basic authentication log structures

## Outcome

Successfully created and populated a PostgreSQL security monitoring database on Ubuntu Linux.

This lab establishes the foundation for further SQL-based security investigations and database auditing.

---

**Project:** SQL for Cloud Security  
**Day:** 01  
**Status:** Completed
