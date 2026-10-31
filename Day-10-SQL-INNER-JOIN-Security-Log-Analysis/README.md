# Day 10 – SQL INNER JOIN and Security Log Analysis

## Project Overview

This lab focuses on combining relational database tables using SQL INNER JOIN in PostgreSQL.

The objective was to connect user account information with security event records, investigate individual user activities, analyse login and password-change events, and calculate event counts using aggregate functions.

The lab demonstrates how SQL JOIN operations can help security professionals correlate user identities with recorded activities during security investigations.

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

The `users.id` column is related to the `events.user_id` column.

## Tasks Completed

### 1. Review Database Tables

Retrieved records from the users table.

```
SELECT *
FROM users;
```

Retrieved security event records.

```
SELECT *
FROM events;
```

Reviewed user account information and recorded activities before performing JOIN operations.

### 2. Perform INNER JOIN Between Users and Events

Combined the users and events tables using INNER JOIN.

```
SELECT
    u.username,
    u.email,
    e.event_type,
    e.ts
FROM users u
INNER JOIN events e
ON u.id = e.user_id;
```

This query combines user account information with corresponding security event records.

### 3. Investigate Events Associated with a Specific User

Filtered joined records using a specific email address.

```
SELECT
    u.email,
    e.event_type,
    e.ts
FROM users u
INNER JOIN events e
ON u.id = e.user_id
WHERE u.email = 'sri@gmail.com';
```

This helps investigate the activities associated with an individual user account.

### 4. Investigate Login Events

Retrieved login activities from the joined tables.

```
SELECT
    u.email,
    e.event_type,
    e.ts
FROM users u
INNER JOIN events e
ON u.id = e.user_id
WHERE e.event_type = 'login'
ORDER BY e.ts DESC;
```

Reviewed login activities and their corresponding timestamps.

### 5. Investigate Password Change Events

Filtered records to identify password-change activities.

```
SELECT
    u.email,
    e.event_type,
    e.ts
FROM users u
INNER JOIN events e
ON u.id = e.user_id
WHERE e.event_type = 'password_change';
```

The query returned two password-change event records in the lab dataset.

### 6. Investigate File Upload Events

Filtered joined records to identify file-upload activities.

```
SELECT
    u.username,
    u.email,
    e.event_type,
    e.ts
FROM users u
INNER JOIN events e
ON u.id = e.user_id
WHERE e.event_type = 'file_upload';
```

This helps identify which user account is associated with a recorded file-upload event.

### 7. Count Total Security Events

Used COUNT() to calculate the total number of recorded events.

```
SELECT
    COUNT(*) AS total_events
FROM events;
```

The query returned seven event records in the lab dataset.

### 8. Count Events by Event Type

Used GROUP BY and COUNT() to calculate the number of events in each category.

```
SELECT
    event_type,
    COUNT(*) AS total
FROM events
GROUP BY event_type;
```

Analysed event categories such as:

- Login
- File upload
- File download
- Password change

### 9. Count Events Associated with Each User

Combined INNER JOIN, COUNT(), and GROUP BY to calculate event totals for individual users.

```
SELECT
    u.email,
    COUNT(e.id) AS total_events
FROM users u
INNER JOIN events e
ON u.id = e.user_id
GROUP BY u.email;
```

This query helps understand how many recorded events are associated with each user account.

## Security Relevance

SQL JOIN operations are useful in cloud security monitoring, database auditing, and incident response.

These techniques help security professionals:

- Correlate user accounts with security events.
- Investigate individual user activities.
- Identify accounts associated with password changes.
- Review login and file-upload activities.
- Calculate event counts by category.
- Analyse user activity patterns.
- Support security investigations using relational data.

**Important:** An event record provides evidence of an activity, but additional investigation is required to determine whether the activity was unauthorized or malicious.

## Screenshots

| Screenshot | Description |
|---|---|
| 01-users-and-events-table-review.png | Reviewing users and events tables |
| 02-inner-join-user-event-analysis.png | Combining user and event records |
| 03-user-event-count-and-group-by.png | Counting events associated with users |
| 04-filter-user-and-event-records.png | Filtering user-specific event records |
| 05-login-and-password-change-investigation.png | Investigating login and password-change events |
| 06-event-count-and-security-analysis.png | Counting and grouping security events |

## Key Learning Outcomes

- Understanding relational database relationships.
- Performing SQL INNER JOIN operations.
- Using table aliases.
- Connecting primary and foreign key columns.
- Combining user and event records.
- Filtering joined records using WHERE.
- Sorting event records using ORDER BY.
- Counting records using COUNT().
- Grouping records using GROUP BY.
- Investigating login, password-change, and file-upload activities.

## Outcome

Successfully performed SQL INNER JOIN operations to correlate user account information with security event records.

Applied JOIN, WHERE, ORDER BY, COUNT(), and GROUP BY to investigate user activities and analyse security event patterns.

This lab provides practical foundations for relational database analysis, security log correlation, and cloud security investigations.

---

**Project:** SQL for Cloud Security  
**Day:** 10  
**Status:** Completed
