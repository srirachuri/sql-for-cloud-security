# Day 15 – SQL Subqueries and User Activity Analysis

## Project Overview

This lab focuses on using SQL subqueries in PostgreSQL to investigate user accounts and their associated security event records.

The objective was to identify users with recorded activities, find accounts without matching events, investigate specific event types, and calculate active user counts using nested SQL queries.

The lab demonstrates how IN, NOT IN, and nested SELECT statements can support user account investigations and security monitoring.

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

## Tasks Completed

### 1. Identify Users with Recorded Security Events

Used IN with a subquery to retrieve email addresses of users who have matching security event records.

```
SELECT email
FROM users
WHERE id IN (
    SELECT user_id
    FROM events
);
```

The query returned seven user accounts with recorded events.

This demonstrates how a subquery can retrieve matching user IDs from another table.

### 2. Identify Users Without Recorded Security Events

Used NOT IN to identify user accounts without matching event records.

```
SELECT username, email
FROM users
WHERE id NOT IN (
    SELECT user_id
    FROM events
);
```

The lab identified:

- Username: temp_employee
- Email: temp.employee@company.com

This technique helps identify accounts without recorded security activities.

### 3. Investigate Password Change Events

Used a subquery to identify users associated with password-change events.

```
SELECT username, email
FROM users
WHERE id IN (
    SELECT user_id
    FROM events
    WHERE event_type = 'password_change'
);
```

The query returned two user accounts:

- john.doe – john.doe@company.com
- admin – bob.smith@company.com

This helps identify accounts associated with recorded password-change activities.

### 4. Investigate File Upload Activities

Used a subquery to retrieve users associated with file-upload events.

```
SELECT username, email
FROM users
WHERE id IN (
    SELECT user_id
    FROM events
    WHERE event_type = 'file_upload'
);
```

The lab identified:

- sri – sri@gmail.com
- gabriel – gabriel@company.com

### 5. Investigate Login Activities

Retrieved users associated with login events.

```
SELECT username, email
FROM users
WHERE id IN (
    SELECT user_id
    FROM events
    WHERE event_type = 'login'
);
```

The query returned three user accounts:

- sri – sri@gmail.com
- test – test@yahoo.com
- eil – eil@yahoo.com

### 6. Count Active Users

Used COUNT() with a subquery to calculate the number of users with recorded security events.

```
SELECT
    COUNT(*) AS active_users
FROM users
WHERE id IN (
    SELECT user_id
    FROM events
);
```

**Result:** 7 active users with recorded events.

### 7. Filter Gmail Accounts with Recorded Events

Combined LIKE and IN to identify Gmail accounts associated with security events.

```
SELECT username, email
FROM users
WHERE email LIKE '%gmail.com'
AND id IN (
    SELECT user_id
    FROM events
);
```

The query returned:

- sri – sri@gmail.com
- noah – noah@gmail.com

This demonstrates how multiple filtering conditions can be combined with a subquery.

### 8. Count Events Associated with Existing User Accounts

Used IN with a subquery to count event records whose user IDs match existing user accounts.

```
SELECT
    COUNT(*) AS total_users
FROM events
WHERE user_id IN (
    SELECT id
    FROM users
);
```

**Result:** 8 matching event records.

This query counts matching event records, not unique users.

## Security Relevance

SQL subqueries are useful in cloud security monitoring, database auditing, and user activity investigations.

These techniques help security professionals:

- Identify users with recorded security activities.
- Find accounts without matching event records.
- Investigate password-change activities.
- Identify users associated with file uploads.
- Review accounts associated with login events.
- Calculate active user counts.
- Combine multiple filtering conditions.
- Perform nested database investigations.

**Security consideration:** Accounts without recorded events are not automatically suspicious. Additional investigation of account status, permissions, and logging completeness is necessary.

## Screenshots

| Screenshot | Description |
|---|---|
| 01-in-and-not-in-user-investigation.png | Identifying users with and without recorded events |
| 02-event-type-subquery-analysis.png | Investigating password changes, file uploads, and login activities |
| 03-active-user-count-and-email-filtering.png | Counting active users and filtering Gmail accounts |

## Key Learning Outcomes

- Understanding SQL subqueries.
- Writing nested SELECT statements.
- Using IN with subqueries.
- Using NOT IN with subqueries.
- Identifying users with recorded activities.
- Finding users without matching event records.
- Filtering specific event types.
- Combining LIKE with subqueries.
- Counting active users using COUNT().
- Understanding relationships between users and events.

## Outcome

Successfully practised SQL subqueries using PostgreSQL.

Applied IN, NOT IN, nested SELECT statements, LIKE, and COUNT() to investigate user accounts, password changes, file uploads, login activities, and active user records.

This lab provides practical foundations for advanced SQL querying, database auditing, and cloud security investigations.

---

**Project:** SQL for Cloud Security  
**Day:** 15  
**Status:** Completed
