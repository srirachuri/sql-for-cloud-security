# Day 6 – Recent Login Activity Analysis Using SQL

## Project Overview

This lab focuses on analysing recent user activity and authentication records using PostgreSQL.

The objective was to organise database records by timestamps, retrieve the latest login activities, limit query results, skip selected records, and investigate user-related security events.

SQL ORDER BY, LIMIT, and OFFSET clauses were used to build a basic recent activity analysis workflow.

## Environment

- Operating System: Ubuntu Linux
- Virtualisation: Oracle VirtualBox
- Database: PostgreSQL 17
- Database Name: `security_lab`
- Interface: PostgreSQL Command Line (psql)

## Tasks Completed

### 1. Sort User Records Using ORDER BY

Retrieved user records and sorted them by creation date in descending order.

```
SELECT *
FROM users
ORDER BY created_at DESC;
```

This displays the most recently created user records first.

### 2. Sort Records in Ascending Order

I used ASC to display records in ascending order.

```
SELECT *
FROM auth_logs
ORDER BY ts ASC;
```

This helps review authentication records from oldest to newest.

### 3. Retrieve Recent Records Using LIMIT

I used LIMIT to restrict the number of records returned.

```
SELECT *
FROM users
ORDER BY created_at DESC
LIMIT 3;
```

This retrieves the three most recently created user records.

### 4. Use OFFSET to Skip Records

I used OFFSET to skip a specified number of records.

```
SELECT *
FROM users
ORDER BY created_at DESC
LIMIT 2 OFFSET 1;
```

This skips the first record and retrieves the next two records.

### 5. Investigate Recent Authentication Activity

Retrieved the latest authentication records.

```
SELECT *
FROM auth_logs
ORDER BY ts DESC
LIMIT 3;
```

This helps identify the most recent authentication activities.

### 6. Filter Failed Login Attempts

I combined WHERE, ORDER BY, and LIMIT to investigate recent failed login attempts.

```
SELECT *
FROM auth_logs
WHERE status = 'FAIL'
ORDER BY ts DESC
LIMIT 5;
```

This retrieves the five most recent failed authentication records.

### 7. Review User Event Activity

Retrieved event records associated with a specific user.

```
SELECT *
FROM events
WHERE user_id = 1
ORDER BY ts DESC
LIMIT 3;
```

Reviewed recorded activities such as:

- Login events
- File upload activities
- Password changes

### 8. Investigate Password Change Events

Filtered the events table to retrieve password-change activities.

```
SELECT *
FROM events
WHERE event_type = 'password_change'
ORDER BY ts DESC;
```

This helps review password-related events recorded in the database.

## Security Relevance

Recent activity analysis is useful in cloud security monitoring and incident response.

These SQL techniques help security professionals:

- Retrieve the latest authentication records.
- Review recent failed login attempts.
- Investigate user activity timelines.
- Identify recent password-change events.
- Sort security records by timestamps.
- Focus investigations on relevant database records.
- Reduce unnecessary query output using LIMIT and OFFSET.

**Note:** Recent or failed authentication events are investigation indicators, not proof of malicious activity.

## Screenshots

| Screenshot | Description |
|---|---|
| 01-user-records-sorting.png | Sorting user records by creation date |
| 02-authentication-log-sorting.png | Sorting authentication logs |
| 03-limit-and-offset-queries.png | Practising LIMIT and OFFSET |
| 04-recent-login-activity.png | Retrieving recent login records |
| 05-user-event-activity-analysis.png | Reviewing user events and password changes |

## Key Learning Outcomes

- Understanding SQL ORDER BY.
- Sorting records using ASC and DESC.
- Retrieving recent records using LIMIT.
- Skipping records using OFFSET.
- Sorting authentication logs by timestamps.
- Filtering failed login attempts.
- Reviewing user activity records.
- Investigating password-change events.
- Building basic SQL-based activity analysis workflows.

## Outcome

Successfully practised SQL sorting, pagination, and recent activity analysis using PostgreSQL.

Applied ORDER BY, LIMIT, OFFSET, and WHERE clauses to retrieve and investigate user activity, authentication logs, and security-related events.

This lab provides a foundation for security log analysis, incident investigation, and database monitoring.

---

**Project:** SQL for Cloud Security  
**Day:** 06  
**Status:** Completed
