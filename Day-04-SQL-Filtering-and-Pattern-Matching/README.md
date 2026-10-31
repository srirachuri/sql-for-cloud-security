# Day 4 – SQL Filtering and Pattern Matching

## Project Overview

This lab focuses on filtering database records and searching for specific information using SQL WHERE, LIKE, AND, and OR operators in PostgreSQL.

The objective was to retrieve targeted employee account records, search email addresses using pattern matching, and investigate authentication logs based on IP addresses and login statuses.

## Environment

- Operating System: Ubuntu Linux
- Virtualisation: Oracle VirtualBox
- Database: PostgreSQL 17
- Database Name: `security_lab`
- Interface: PostgreSQL Command Line (psql)

## Tasks Completed

### 1. Filter Records Using WHERE

Used the WHERE clause to retrieve records that match specific conditions.

```
SELECT *
FROM users
WHERE id = 1;
```

Practised filtering records using comparison operators.

```
SELECT *
FROM users
WHERE id > 1;
```

### 2. Search Email Addresses Using LIKE

Used the LIKE operator to search for email addresses matching specific patterns.

```
SELECT *
FROM users
WHERE email LIKE '%gmail.com';
```

Searched for email addresses associated with other domains.

```
SELECT *
FROM users
WHERE email LIKE '%yahoo.com';
```

Also practised searching for specific text patterns.

```
SELECT *
FROM users
WHERE email LIKE '%admin';
```

```
SELECT *
FROM users
WHERE email LIKE '%sri%';
```

### 3. Filter Authentication Logs Using AND

Used the AND operator to retrieve authentication records that satisfy multiple conditions simultaneously.

```
SELECT *
FROM auth_logs
WHERE ip = '192.168.1.10'
AND status = 'FAIL';
```

This query retrieves failed authentication attempts associated with a specific IP address.

### 4. Filter Authentication Logs Using OR

Used the OR operator to retrieve records matching either of the specified conditions.

```
SELECT *
FROM auth_logs
WHERE ip = '192.168.1.10'
OR ip = '10.0.0.5';
```

This query retrieves authentication records associated with either IP address.

### 5. Analyse Authentication Records

Reviewed the retrieved authentication records to understand:

- Source IP addresses.
- Successful authentication attempts.
- Failed authentication attempts.
- Multiple login attempts from the same IP address.

## Security Relevance

SQL filtering and pattern matching are important techniques in security monitoring and incident investigation.

These techniques help security professionals:

- Identify specific employee accounts.
- Search for email address patterns.
- Filter failed login attempts.
- Investigate authentication activity from specific IP addresses.
- Identify potentially suspicious login patterns.
- Narrow down security events during incident investigations.

**Note:** A failed login or an unfamiliar IP address alone does not establish malicious activity. Additional investigation is required.

## Screenshots

| Screenshot | Description |
|---|---|
| 01-where-clause-and-basic-filtering.png | Filtering user records using WHERE |
| 02-like-pattern-matching.png | Searching email addresses using LIKE |
| 03-and-or-authentication-log-analysis.png | Filtering authentication logs using AND and OR |

## Key Learning Outcomes

- Using the SQL WHERE clause.
- Filtering records with comparison operators.
- Searching text using LIKE.
- Understanding SQL wildcard characters.
- Combining conditions using AND.
- Combining alternative conditions using OR.
- Filtering authentication logs.
- Applying SQL queries to security investigations.

## Outcome

Successfully practised SQL filtering, pattern matching, and conditional operators using PostgreSQL.

These techniques provide a foundation for analysing authentication logs, investigating suspicious account activity, and performing database security audits.

---

**Project:** SQL for Cloud Security  
**Day:** 04  
**Status:** Completed
