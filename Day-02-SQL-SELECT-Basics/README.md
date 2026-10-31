# Day 2 – SQL SELECT Statements and Data Retrieval

## Project Overview

This lab focuses on learning SQL SELECT statements in PostgreSQL to retrieve and analyse information from relational database tables.

The objective was to understand how to retrieve all records, select specific columns, and access user information, system events, and authentication logs in a simulated security monitoring environment.

## Environment

- Operating System: Ubuntu Linux
- Virtualisation: Oracle VirtualBox
- Database: PostgreSQL 17
- Database Name: `security_lab`
- Interface: PostgreSQL Command Line (psql)

## Tasks Completed

### 1. Retrieve All Records

Used SELECT * to retrieve all records from database tables.

```
SELECT * FROM users;

SELECT * FROM events;

SELECT * FROM auth_logs;
```

### 2. Retrieve Specific Columns

I practised selecting individual columns instead of retrieving entire records.

```
SELECT username FROM users;

SELECT email FROM users;

SELECT id, email FROM users;

SELECT username, email FROM users;
```

### 3. Retrieve User Information

Retrieved usernames and email addresses from the users table.

This helped me understand how to access specific user account information stored in a database.

### 4. Retrieve Security Events

Queried the events table to examine recorded activities.

```
SELECT * FROM events;
```

Reviewed sample activities such as:
- Login
- File upload
- Password change

### 5. Retrieve Authentication Logs

Queried the authentication logs table.

```
SELECT * FROM auth_logs;
```

Reviewed sample authentication records containing:
- Log ID
- IP address
- Authentication status
- Timestamp

Observed successful and failed authentication attempts.

## Security Relevance

SQL SELECT statements support security monitoring and incident investigations.

They help security professionals:

- Review user account information.
- Examine authentication activities.
- Identify failed login attempts.
- Review suspicious IP addresses.
- Investigate recorded system events.
- Retrieve relevant information during security audits.

## Screenshots

| Screenshot | Description |
|---|---|
| 01-select-all-records.png | Retrieving all records using SELECT * |
| 02-select-specific-columns.png | Selecting individual database columns |
| 03-retrieve-security-logs.png | Retrieving user, event, and authentication records |

## Key Learning Outcomes

- Understanding SQL SELECT statements.
- Retrieving all records using SELECT *.
- Selecting individual columns.
- Querying multiple database tables.
- Accessing user account information.
- Reading authentication logs.
- Understanding the role of SQL in security investigations.

## Outcome

Successfully practised SQL SELECT statements and retrieved information from PostgreSQL database tables.

This lab established the foundation for more advanced SQL querying, filtering, security log analysis, and suspicious activity investigations.

---

**Project:** SQL for Cloud Security  
**Day:** 02  
**Status:** Completed
