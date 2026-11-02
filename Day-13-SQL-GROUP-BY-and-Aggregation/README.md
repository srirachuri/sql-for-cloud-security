# Day 13 – SQL GROUP BY and Aggregate Functions for Security Analysis

## Project Overview

This lab focuses on analysing user accounts, authentication logs, and security events using SQL aggregate functions and GROUP BY in PostgreSQL.

The objective was to calculate record counts, analyse authentication statuses, identify IP addresses associated with successful and failed login attempts, calculate event totals by category, and investigate user activity patterns.

The lab also demonstrates the use of HAVING, COUNT(), SUM(), and AVG() to perform database analysis and security monitoring.

## Environment

- Operating System: Ubuntu Linux
- Virtualisation: Oracle VirtualBox
- Database: PostgreSQL 17
- Database Name: `security_lab`
- Interface: PostgreSQL Command Line (psql)

## Database Tables

### Users Table

Contains user account information.

- id
- username
- email
- created_at

### Events Table

Contains recorded user activities.

- id
- user_id
- event_type
- ts

### Authentication Logs Table

Contains authentication records.

- id
- ip
- status
- ts

## Tasks Completed

### 1. Count Total User Accounts

Used COUNT() to calculate the total number of user accounts.

```
SELECT COUNT(*) AS total_users
FROM users;
```

**Result:** 8 user records.

### 2. Count Total Security Events

Calculated the total number of records in the events table.

```
SELECT COUNT(*) AS total_events
FROM events;
```

**Result:** 8 event records.

### 3. Count Total Authentication Logs

Retrieved the total number of authentication log records.

```
SELECT COUNT(*) AS total_logs
FROM auth_logs;
```

**Result:** 6 authentication records.

### 4. Calculate the Sum of User IDs

Used SUM() to calculate the total of user ID values.

```
SELECT SUM(id) AS total_user_ids
FROM users;
```

**Result:** 39.

### 5. Calculate the Average User ID

Used AVG() to calculate the average user ID.

```
SELECT AVG(id) AS average_user_id
FROM users;
```

**Result:** 4.875.

This exercise demonstrated the use of aggregate functions for numerical calculations.

### 6. Count Events by User ID

Used GROUP BY to calculate the number of events associated with each user ID.

```
SELECT
    user_id,
    COUNT(*) AS event_count
FROM events
GROUP BY user_id
ORDER BY event_count DESC;
```

This query helps identify users with higher numbers of recorded events.

### 7. Count Events by Username

Combined LEFT JOIN, COUNT(), and GROUP BY to calculate event totals for every user.

```
SELECT
    u.username,
    COUNT(e.id) AS total_events
FROM users u
LEFT JOIN events e
ON u.id = e.user_id
GROUP BY u.username
ORDER BY total_events DESC;
```

The lab results included:

- sri – 2 events
- gabriel – 1 event
- test – 1 event
- eil – 1 event
- admin – 1 event
- noah – 1 event
- john.doe – 1 event
- temp_employee – 0 events

### 8. Identify Users Without Recorded Events Using HAVING

Used HAVING to filter grouped results and identify users with zero events.

```
SELECT
    u.username,
    COUNT(e.id) AS total_events
FROM users u
LEFT JOIN events e
ON u.id = e.user_id
GROUP BY u.username
HAVING COUNT(e.id) = 0;
```

The lab identified:

- temp_employee – 0 events.

This demonstrates how HAVING can filter aggregate results.

### 9. Calculate Average Events Per Active User

Used a subquery with AVG() to calculate the average number of events per user represented in the events table.

```
SELECT AVG(event_count) AS average_events
FROM (
    SELECT
        user_id,
        COUNT(*) AS event_count
    FROM events
    GROUP BY user_id
) AS user_events;
```

**Result:** Approximately 1.142857 events per user.

### 10. Count Successful Authentication Attempts by IP Address

Grouped authentication records by IP address and counted successful login attempts.

```
SELECT
    ip,
    COUNT(*) AS successful_attempts
FROM auth_logs
WHERE status = 'SUCCESS'
GROUP BY ip
ORDER BY successful_attempts DESC;
```

The lab identified successful authentication records from:

- 10.0.0.5 – 1 attempt
- 10.0.0.9 – 1 attempt

### 11. Count Authentication Attempts by Status

Used GROUP BY to compare successful and failed authentication records.

```
SELECT
    status,
    COUNT(*) AS total
FROM auth_logs
GROUP BY status;
```

The lab results were:

- SUCCESS – 2 records
- FAIL – 4 records

### 12. Count Security Events by Event Type

Grouped the events table by event_type.

```
SELECT
    event_type,
    COUNT(*) AS total_events
FROM events
GROUP BY event_type
ORDER BY total_events DESC;
```

The lab results were:

- login – 3 events
- file_upload – 2 events
- password_change – 2 events
- file_download – 1 event

### 13. Count Failed Login Attempts by IP Address

Used WHERE, GROUP BY, and COUNT() to investigate failed authentication attempts.

```
SELECT
    ip,
    COUNT(*) AS failed_attempts
FROM auth_logs
WHERE status = 'FAIL'
GROUP BY ip
ORDER BY failed_attempts DESC;
```

The lab results showed:

- 192.168.1.10 – 2 failed attempts
- 172.16.0.15 – 1 failed attempt
- 192.168.1.01 – 1 failed attempt

These results help identify IP addresses associated with multiple failed authentication attempts.

## Security Relevance

SQL aggregation and grouping are useful in cloud security monitoring, SOC operations, and database auditing.

These techniques help security professionals:

- Count successful and failed authentication attempts.
- Identify IP addresses associated with repeated failed logins.
- Analyse authentication status patterns.
- Calculate user activity totals.
- Identify accounts without recorded events.
- Monitor login and file-upload activities.
- Investigate password-change events.
- Summarise large volumes of security records.

**Security consideration:** Repeated failed login attempts may indicate suspicious activity, but additional investigation is required before classifying an IP address as malicious.

## Screenshots

| Screenshot | Description |
|---|---|
| 01-user-event-counts-and-grouping.png | Counting events by user ID |
| 02-left-join-and-having-analysis.png | Using LEFT JOIN and HAVING to identify users without events |
| 03-authentication-and-event-type-counts.png | Analysing authentication statuses and event categories |
| 04-user-and-ip-address-aggregation.png | Grouping user activity and failed login attempts by IP |
| 05-database-count-sum-and-average.png | Practising COUNT(), SUM(), and AVG() |

## Key Learning Outcomes

- Understanding SQL aggregate functions.
- Counting records using COUNT().
- Calculating totals using SUM().
- Calculating averages using AVG().
- Grouping records using GROUP BY.
- Filtering grouped results using HAVING.
- Combining LEFT JOIN with aggregate functions.
- Counting successful and failed authentication attempts.
- Analysing login activity by IP address.
- Counting security events by event type.
- Investigating user activity patterns.

## Outcome

Successfully practised SQL aggregation and grouping operations using PostgreSQL.

Applied COUNT(), SUM(), AVG(), GROUP BY, HAVING, and LEFT JOIN to analyse user accounts, security events, and authentication logs.

This lab provides practical foundations for security log analysis, database auditing, and cloud security monitoring.

---

**Project:** SQL for Cloud Security  
**Day:** 13  
**Status:** Completed
