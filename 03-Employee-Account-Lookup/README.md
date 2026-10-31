# Day 3 – Employee Account Lookup Using SQL

## Project Overview

This lab focuses on retrieving and filtering employee account information using PostgreSQL.

The objective was to practise SQL queries for looking up individual user accounts, retrieving email addresses, filtering records, and reviewing related security events and authentication logs.

## Environment

- Operating System: Ubuntu Linux
- Virtualisation: Oracle VirtualBox
- Database: PostgreSQL 17
- Database Name: `security_lab`
- Interface: PostgreSQL Command Line (psql)

## Tasks Completed

### 1. Connect to PostgreSQL

Connected to the PostgreSQL database using the Linux terminal.

```
sudo -u postgres psql
```

Connected to the security database:

```
\c security_lab
```

### 2. Retrieve Employee Account Information

Retrieved all user account records from the users table.

```
SELECT *
FROM users;
```

### 3. Retrieve Specific Email Addresses

Selected email addresses from the users table.

```
SELECT email
FROM users;
```

### 4. Use Column Aliases

Used the SQL AS keyword to rename a column in query results.

```
SELECT email AS user_email
FROM users;
```

### 5. Filter Employee Accounts Using WHERE

Used the WHERE clause to retrieve a specific employee account based on an email address.

```
SELECT *
FROM users
WHERE email = 'sri@gmail.com';
```

This demonstrates how to locate an individual account instead of retrieving every user record.

### 6. Review Related Security Records

Retrieved event records:

```
SELECT *
FROM events;
```

Retrieved authentication records:

```
SELECT *
FROM auth_logs;
```

Reviewed sample login activities and authentication statuses, including successful and failed attempts.

## Security Relevance

Employee account lookup is useful in cloud security operations and database investigations.

Security professionals can use these techniques to:

- Locate specific user accounts.
- Investigate employee account activity.
- Retrieve account-related information.
- Review authentication records.
- Investigate failed login attempts.
- Support security audits and incident investigations.

## Screenshots

| Screenshot | Description |
|---|---|
| 01-employee-account-queries.png | Employee account retrieval and SQL queries |
| 02-filtered-user-and-security-records.png | Email filtering and security record review |

## Key Learning Outcomes

- Connecting to PostgreSQL databases.
- Retrieving employee account information.
- Selecting specific database columns.
- Using column aliases with AS.
- Filtering records using WHERE.
- Looking up individual user accounts.
- Reviewing authentication and event records.

## Outcome

Successfully practised employee account lookup and record filtering using PostgreSQL.

These SQL techniques provide a foundation for investigating user activity, analysing authentication logs, and auditing database security.

---

**Project:** SQL for Cloud Security  
**Day:** 03  
**Status:** Completed
