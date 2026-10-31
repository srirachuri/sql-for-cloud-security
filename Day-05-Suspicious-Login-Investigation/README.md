# Day 5 – Investigating Suspicious Login Attempts Using SQL

## Project Overview

This lab focuses on investigating authentication records and identifying potentially suspicious login activity using PostgreSQL.

The objective was to analyse failed login attempts, filter authentication records by IP address, apply comparison operators, and combine multiple SQL conditions to investigate login activity.

## Environment

- Operating System: Ubuntu Linux
- Virtualisation: Oracle VirtualBox
- Database: PostgreSQL 17
- Database Name: `security_lab`
- Interface: PostgreSQL Command Line (psql)

## Tasks Completed

### 1. Identify Failed Login Attempts

Retrieved authentication records with failed login status.

```
SELECT *
FROM auth_logs
WHERE status = 'FAIL';
```

This query helps identify unsuccessful authentication attempts.

### 2. Investigate Login Activity by IP Address

Filtered authentication logs using a specific IP address.

```
SELECT *
FROM auth_logs
WHERE ip = '192.168.1.10';
```

Reviewed authentication activity associated with the selected IP address.

### 3. Combine Conditions Using AND

Combined IP address and authentication status conditions.

```
SELECT *
FROM auth_logs
WHERE ip = '192.168.1.10'
AND status = 'FAIL';
```

This query retrieves failed login attempts associated with a specific IP address.

### 4. Combine Conditions Using OR

I used OR to investigate activity from multiple IP addresses.

```
SELECT *
FROM auth_logs
WHERE ip = '192.168.1.10'
OR ip = '10.0.0.5';
```

This helps retrieve authentication records from either IP address.

### 5. Apply Comparison Operators

Used comparison operators to filter user records.

```
SELECT *
FROM users
WHERE id > 1;
```

Also practised retrieving records using less-than-or-equal-to conditions.

```
SELECT *
FROM users
WHERE id <= 2;
```

### 6. Search Email Addresses Using LIKE

Used pattern matching to retrieve email addresses.

```
SELECT email
FROM users
WHERE email LIKE '%.com';
```

This retrieves email addresses ending with `.com`.

### 7. Analyse Authentication Results

Reviewed the sample authentication records.

Observed:
- IP address `192.168.1.10` had failed authentication attempts.
- IP address `10.0.0.5` had a successful authentication record.
- Multiple failed login records were associated with the same IP address.

These observations demonstrate how SQL can help identify login patterns that may require further investigation.

## Security Relevance

Investigating authentication logs is an important activity in cloud security and Security Operations Centre (SOC) environments.

These techniques help security professionals:

- Identify failed authentication attempts.
- Investigate repeated login failures.
- Analyse activity associated with specific IP addresses.
- Compare successful and unsuccessful login events.
- Filter user and authentication records.
- Support security incident investigations.

**Important:** Repeated failed logins may indicate suspicious activity, but additional evidence is required before classifying an event as an attack.

## Screenshots

| Screenshot | Description |
|---|---|
| 01-user-and-login-comparison-queries.png | SQL comparison and user filtering |
| 02-failed-login-and-ip-investigation.png | Failed login and IP address investigation |
| 03-suspicious-login-analysis-results.png | Authentication analysis and query results |

## Key Learning Outcomes

- Investigating authentication logs using SQL.
- Identifying failed login attempts.
- Filtering records by IP address.
- Combining conditions using AND and OR.
- Applying SQL comparison operators.
- Searching email addresses using LIKE.
- Comparing successful and failed authentication records.
- Understanding basic security log investigation techniques.

## Outcome

Successfully investigated simulated authentication records using PostgreSQL.

Applied SQL filtering, comparison operators, and conditional queries to identify failed login activity and examine authentication patterns.

This lab provides practical foundations for security monitoring, SOC investigations, and cloud security operations.

---

**Project:** SQL for Cloud Security  
**Day:** 05  
**Status:** Completed
