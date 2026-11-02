# Day 12 – SQL RIGHT JOIN and User Activity Analysis

## Project Overview

This lab focuses on combining relational database tables using SQL RIGHT JOIN in PostgreSQL.

The objective was to retrieve all user accounts alongside their corresponding security event records, identify users without matching events, investigate login and file-upload activities, and calculate event counts for individual accounts.

The lab demonstrates how RIGHT JOIN can support user account auditing and security event investigations.

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

Relationship:

`events.user_id = users.id`

## Tasks Completed

### 1. Perform a RIGHT JOIN Between Users and Events

Combined the events and users tables using a RIGHT JOIN.

```
SELECT *
FROM events e
RIGHT JOIN users u
ON e.user_id = u.id;
```

This query returns all records from the users table and matching records from the events table.

Users without matching events are also included, with NULL values in the event columns.

The query returned nine rows in the lab dataset.

### 2. Retrieve Selected User and Event Information

Selected specific columns from both tables.

```
SELECT
    u.id,
    u.username,
    u.email,
    e.event_type
FROM events e
RIGHT JOIN users u
ON e.user_id = u.id;
```

This makes it easier to review user identities alongside their recorded activities.

### 3. Identify Users Without Recorded Events

Used IS NULL to identify accounts without matching event records.

```
SELECT
    u.username,
    u.email
FROM events e
RIGHT JOIN users u
ON e.user_id = u.id
WHERE e.id IS NULL;
```

The lab identified one account without a matching security event:

- Username: temp_employee
- Email: temp.employee@company.com

This demonstrates how RIGHT JOIN can identify unmatched user records.

### 4. Retrieve Login Events

I filtered the joined records to retrieve login activities.

```
SELECT
    u.username,
    u.email,
    e.event_type
FROM events e
RIGHT JOIN users u
ON e.user_id = u.id
WHERE e.event_type = 'login';
```

The query returned three login event records in the lab dataset.

### 5. Count Events Associated with Each User

Used COUNT() and GROUP BY to calculate the number of events associated with individual users.

```
SELECT
    u.username,
    COUNT(e.id) AS total_events
FROM events e
RIGHT JOIN users u
ON e.user_id = u.id
GROUP BY u.username
ORDER BY total_events DESC;
```

The results showed:

- sri – 2 events
- gabriel – 1 event
- test – 1 event
- eil – 1 event
- admin – 1 event
- noah – 1 event
- john.doe – 1 event
- temp_employee – 0 events

This query also includes users without recorded events.

### 6. Investigate Recently Created User Accounts

Used CURRENT_DATE and INTERVAL to retrieve accounts created within the last 30 days.

```
SELECT
    u.username,
    u.email,
    u.created_at,
    e.event_type
FROM events e
RIGHT JOIN users u
ON e.user_id = u.id
WHERE u.created_at >= CURRENT_DATE - INTERVAL '30 days';
```

Reviewed user creation dates alongside matching security event records.

### 7. Investigate File Upload Activities

Filtered joined records to identify file-upload events.

```
SELECT
    u.username,
    u.email,
    e.event_type,
    e.ts
FROM events e
RIGHT JOIN users u
ON e.user_id = u.id
WHERE e.event_type = 'file_upload';
```

The query returned two file-upload event records associated with user accounts.

### 8. Count Total User Accounts

Used COUNT() to calculate the total number of user records.

```
SELECT COUNT(*)
FROM users;
```

### 9. Count Distinct Users with Recorded Events

Used COUNT(DISTINCT) to count the unique user IDs in the events table.

```
SELECT COUNT(DISTINCT user_id)
FROM events;
```

This helps distinguish the number of unique users with recorded events from the total number of event records.

### 10. Count Users Without Matching Events

Used RIGHT JOIN and IS NULL to calculate the number of users without corresponding event records.

```
SELECT COUNT(*)
FROM events e
RIGHT JOIN users u
ON e.user_id = u.id
WHERE e.id IS NULL;
```

The query returned one user without matching event records.

## Security Relevance

RIGHT JOIN is useful in database auditing, user activity monitoring, and security investigations.

These techniques help security professionals:

- Retrieve all user accounts, including accounts without matching event records.
- Identify accounts with no recorded activities.
- Investigate login and file-upload events.
- Calculate event counts for individual users.
- Compare total accounts with users represented in security logs.
- Investigate recently created accounts.
- Identify potential gaps in event logging.

**Security consideration:** An account without recorded events is not automatically suspicious. Also review account status, permissions, authentication history, and logging completeness.

## Screenshots

| Screenshot | Description |
|---|---|
| 01-right-join-users-and-events.png | Combining users and events using RIGHT JOIN |
| 02-identifying-users-without-events.png | Identifying accounts without matching events |
| 03-login-events-and-user-event-counts.png | Investigating login events and counting user activities |
| 04-recent-user-and-security-event-analysis.png | Reviewing recently created accounts and security events |
| 05-file-upload-and-event-count-analysis.png | Investigating file uploads and calculating event counts |

## Key Learning Outcomes

- Understanding SQL RIGHT JOIN.
- Understanding RIGHT JOIN versus INNER JOIN and LEFT JOIN.
- Combining relational database tables.
- Identifying unmatched records using IS NULL.
- Filtering login and file-upload events.
- Counting records using COUNT().
- Counting unique users using COUNT(DISTINCT).
- Grouping records using GROUP BY.
- Sorting event counts using ORDER BY.
- Investigating user accounts without recorded activities.

## Outcome

Successfully performed SQL RIGHT JOIN operations to correlate user account information with security event records.

Applied RIGHT JOIN, IS NULL, WHERE, COUNT(), COUNT(DISTINCT), and GROUP BY to investigate user activities, identify accounts without recorded events, and analyse security event patterns.

This lab provides practical foundations for database auditing, user activity monitoring, and cloud security investigations.

---

**Project:** SQL for Cloud Security  
**Day:** 12  
**Status:** Completed
