# Day 11 – SQL LEFT JOIN and User Activity Analysis

## Project Overview

This lab focuses on using SQL LEFT JOIN operations to investigate user accounts and their associated security event records in PostgreSQL.

The objective was to identify users with and without recorded activities, analyse event counts for individual accounts, investigate newly created accounts, and understand how LEFT JOIN helps detect records without matching entries in related tables.

## Environment

- Operating System: Ubuntu Linux
- Virtualisation: Oracle VirtualBox
- Database: PostgreSQL 17
- Database Name: `security_lab`
- Interface: PostgreSQL Command Line (psql)

## Database Tables

### Users Table

Contains employee and user account information.

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

`users.id = events.user_id`

## Tasks Completed

### 1. Review Users and Events Tables

Retrieved all user records.

```
SELECT *
FROM users
ORDER BY id;
```

Retrieved all security event records.

```
SELECT *
FROM events
ORDER BY id;
```

Reviewed user account information and corresponding security events.

### 2. Perform LEFT JOIN Between Users and Events

Combined the users and events tables using LEFT JOIN.

```
SELECT
    u.email,
    e.event_type,
    e.ts
FROM users u
LEFT JOIN events e
ON u.id = e.user_id
ORDER BY u.email;
```

This query returns all users, including those without matching security event records.

When no matching event exists, the event columns contain NULL values.

### 3. Identify Users Without Recorded Events

I used IS NULL to identify user accounts that do not have matching event records.

```
SELECT
    u.email
FROM users u
LEFT JOIN events e
ON u.id = e.user_id
WHERE e.id IS NULL;
```

The lab identified two user accounts without matching events:

- temp.employee@company.com
- gabriel@company.com

This demonstrates how LEFT JOIN can identify accounts without recorded activity in the events table.

### 4. Retrieve User Creation Dates Without Events

Combined LEFT JOIN with date information to investigate accounts without recorded events.

```
SELECT
    u.email,
    u.created_at
FROM users u
LEFT JOIN events e
ON u.id = e.user_id
WHERE e.id IS NULL;
```

This query displays the creation timestamps of accounts without matching event records.

### 5. Count Events for Every User

Used COUNT() and GROUP BY to calculate the number of recorded events for each user.

```
SELECT
    u.email,
    COUNT(e.id) AS total_events
FROM users u
LEFT JOIN events e
ON u.id = e.user_id
GROUP BY u.email
ORDER BY total_events ASC;
```

This query includes users with zero recorded events.

The lab identified:

- temp.employee@company.com – 0 events
- gabriel@company.com – 0 events

Other users had one or more recorded events.

### 6. Investigate a Specific User's Activities

Filtered the LEFT JOIN results using an email address.

```
SELECT
    u.email,
    e.event_type,
    e.ts
FROM users u
LEFT JOIN events e
ON u.id = e.user_id
WHERE u.email = 'sri@gmail.com';
```

The query returned two recorded activities associated with the selected account:

- login
- file_upload

### 7. Investigate Recently Created Accounts Without Events

Used date filtering alongside LEFT JOIN to identify accounts created within the last 30 days without matching event records.

```
SELECT
    u.email,
    u.created_at
FROM users u
LEFT JOIN events e
ON u.id = e.user_id
WHERE e.id IS NULL
AND u.created_at >= CURRENT_DATE - INTERVAL '30 days';
```

This query helps identify recently created accounts without corresponding event records.

## Security Relevance

LEFT JOIN is useful in cloud security monitoring, user account auditing, and database investigations.

These techniques help security professionals:

- Identify accounts without recorded activities.
- Investigate newly created user accounts.
- Identify users with zero recorded events.
- Compare user records with security event records.
- Find missing relationships between database tables.
- Review account activity during security audits.
- Investigate possible gaps in event logging.

**Security consideration:** An account without recorded events is not necessarily unauthorised or compromised. Additional checks, such as account status, permissions, login history, and audit log completeness, are necessary.

## Screenshots

| Screenshot | Description |
|---|---|
| 01-users-and-events-table-review.png | Reviewing user and event records |
| 02-left-join-user-event-analysis.png | Combining users and events using LEFT JOIN |
| 03-identifying-users-without-events.png | Finding users without matching event records |
| 04-user-event-count-and-zero-activity.png | Counting events for each user |
| 05-filtered-user-activity-investigation.png | Investigating specific user activities |

## Key Learning Outcomes

- Understanding SQL LEFT JOIN.
- Understanding INNER JOIN versus LEFT JOIN.
- Combining relational database tables.
- Identifying unmatched records using IS NULL.
- Counting events using COUNT().
- Grouping records using GROUP BY.
- Sorting results using ORDER BY.
- Filtering specific user accounts.
- Investigating accounts without recorded activities.
- Performing basic user activity audits.

## Outcome

Successfully performed SQL LEFT JOIN operations to investigate user accounts and their associated security event records.

Applied LEFT JOIN, IS NULL, COUNT(), GROUP BY, WHERE, and ORDER BY to identify users without matching events and analyse account activity.

This lab provides a foundation for database auditing, user activity monitoring, and cloud security investigations.

---

**Project:** SQL for Cloud Security  
**Day:** 11  
**Status:** Completed
