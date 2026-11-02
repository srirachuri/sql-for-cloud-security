# Day 16 – SQL EXISTS and NOT EXISTS for Security Investigation

## Project Overview

This lab focuses on using SQL EXISTS and NOT EXISTS operators in PostgreSQL to investigate user accounts and their associated security event records.

The objective was to identify users with recorded activities, find accounts without matching events, investigate password-change and file-upload activities, and filter user accounts based on specific event conditions.

The lab demonstrates how correlated subqueries can support database auditing, user activity monitoring, and security investigations.

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

`users.id = events.user_id`

## Tasks Completed

### 1. Identify Users with Recorded Security Events Using EXISTS

Used EXISTS with a correlated subquery to retrieve users who have matching event records.

```
SELECT u.username, u.email
FROM users u
WHERE EXISTS (
    SELECT 1
    FROM events e
    WHERE e.user_id = u.id
);
```

The query returned seven user accounts with recorded security events.

EXISTS checks whether at least one matching record is present in the events table.

### 2. Identify Users Without Recorded Events Using NOT EXISTS

Used NOT EXISTS to identify user accounts without matching security event records.

```
SELECT u.username, u.email
FROM users u
WHERE NOT EXISTS (
    SELECT 1
    FROM events e
    WHERE e.user_id = u.id
);
```

The lab identified:

- Username: temp_employee
- Email: temp.employee@company.com

This technique helps identify accounts without corresponding event records.

### 3. Investigate Password Change Activities Using EXISTS

I retrieved users associated with password-change events.

```
SELECT u.username, u.email
FROM users u
WHERE EXISTS (
    SELECT 1
    FROM events e
    WHERE e.user_id = u.id
    AND e.event_type = 'password_change'
);
```

The query returned two user accounts:

- john.doe – john.doe@company.com
- admin – bob.smith@company.com

This helps investigate accounts associated with recorded password changes.

### 4. Investigate File Upload Activities Using EXISTS

Identified users associated with file-upload events.

```
SELECT u.username, u.email
FROM users u
WHERE EXISTS (
    SELECT 1
    FROM events e
    WHERE e.user_id = u.id
    AND e.event_type = 'file_upload'
);
```

The lab identified:

- sri – sri@gmail.com
- gabriel – gabriel@company.com

### 5. Investigate Login Activities Using EXISTS

Retrieved users associated with login events.

```
SELECT u.username, u.email
FROM users u
WHERE EXISTS (
    SELECT 1
    FROM events e
    WHERE e.user_id = u.id
    AND e.event_type = 'login'
);
```

This query helps identify accounts with recorded login activities.

### 6. Identify Users Without Password Change Events

Used NOT EXISTS to find users without matching password-change records.

```
SELECT u.username, u.email
FROM users u
WHERE NOT EXISTS (
    SELECT 1
    FROM events e
    WHERE e.user_id = u.id
    AND e.event_type = 'password_change'
);
```

The query returned six user accounts without recorded password-change events.

This demonstrates how NOT EXISTS can filter accounts based on specific event types.

### 7. Identify Users Without File Upload Events

Used NOT EXISTS to retrieve accounts without matching file-upload activities.

```
SELECT u.username, u.email
FROM users u
WHERE NOT EXISTS (
    SELECT 1
    FROM events e
    WHERE e.user_id = u.id
    AND e.event_type = 'file_upload'
);
```

This query helps identify users without recorded file-upload events.

### 8. Filter Gmail Accounts with Recorded Activities

Combined LIKE and EXISTS to identify Gmail accounts with matching security events.

```
SELECT u.username, u.email
FROM users u
WHERE u.email LIKE '%gmail.com'
AND EXISTS (
    SELECT 1
    FROM events e
    WHERE e.user_id = u.id
);
```

The lab identified:

- sri – sri@gmail.com
- noah – noah@gmail.com

This demonstrates how EXISTS can be combined with additional filtering conditions.

## Security Relevance

EXISTS and NOT EXISTS are useful in cloud security monitoring, database auditing, and user activity investigations.

These techniques help security professionals:

- Identify users with recorded security events.
- Find accounts without matching event records.
- Investigate password-change activities.
- Identify users associated with file uploads.
- Review accounts with recorded login activities.
- Find users without specific event types.
- Perform correlated database investigations.
- Support user activity audits.

**Security consideration:** An account without a particular event does not automatically indicate a security problem. Account policies, expected activities, and audit log completeness should also be reviewed.

## Screenshots

| Screenshot | Description |
|---|---|
| 01-exists-and-not-exists-user-analysis.png | Identifying users with and without recorded events |
| 02-password-change-and-login-investigation.png | Investigating password-change and login activities |
| 03-file-upload-and-password-change-filtering.png | Filtering users based on specific event types |
| 04-gmail-user-activity-investigation.png | Filtering Gmail accounts using EXISTS |

## Key Learning Outcomes

- Understanding SQL EXISTS.
- Understanding SQL NOT EXISTS.
- Writing correlated subqueries.
- Checking matching records between relational tables.
- Identifying users without recorded activities.
- Investigating password-change events.
- Investigating file-upload activities.
- Filtering login activity.
- Combining EXISTS with LIKE.
- Understanding the difference between IN and EXISTS.

## Outcome

Successfully practised SQL EXISTS and NOT EXISTS operations using PostgreSQL.

Applied correlated subqueries to investigate user accounts, identify matching security events, find accounts without recorded activities, and analyse password-change, login, and file-upload records.

This lab provides practical foundations for advanced SQL querying, database auditing, and cloud security investigations.

---

**Project:** SQL for Cloud Security  
**Day:** 16  
**Status:** Completed
