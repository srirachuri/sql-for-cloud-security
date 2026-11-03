# Day 20 – SQL Security Dashboard Queries for Cloud Security Monitoring

## Project Overview

This capstone lab focuses on building SQL queries for security monitoring and user activity analysis using PostgreSQL.

The objective was to combine SQL querying, filtering, joins, and aggregate functions to investigate authentication failures, user account activity, and security events.

The lab demonstrates how SQL queries can support a security monitoring dashboard by providing useful information about failed login attempts, inactive accounts, recent user creation, password changes, and file uploads.

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

Contains recorded security activities.

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

### 1. Identify Failed Login Attempts by IP Address

Used WHERE, GROUP BY, and COUNT() to identify IP addresses associated with failed authentication attempts.

```
SELECT
    ip,
    COUNT(*) AS failed_attempts
FROM auth_logs
WHERE status = 'FAIL'
GROUP BY ip
ORDER BY failed_attempts DESC;
```

Results:

- 192.168.1.10 – 2 failed attempts
- 172.16.0.15 – 1 failed attempt
- 192.168.1.01 – 1 failed attempt

This query helps identify IP addresses associated with repeated authentication failures.

### 2. Identify Users Without Recorded Security Events

Used LEFT JOIN and IS NULL to identify accounts without matching event records.

```
SELECT
    u.username,
    u.email
FROM users u
LEFT JOIN events e
ON u.id = e.user_id
WHERE e.id IS NULL;
```

Result:

- temp_employee – temp.employee@company.com

This helps identify accounts without recorded security activity.

### 3. Identify Recently Created User Accounts

I retrieved user accounts created within the previous seven days.

```
SELECT
    id,
    username,
    email,
    created_at
FROM users
WHERE created_at >= CURRENT_DATE - INTERVAL '7 days'
ORDER BY created_at DESC;
```

The query returned eight user records in the lab dataset.

This query helps review recently created accounts during security audits.

### 4. Count Security Events Associated with Each User

Combined LEFT JOIN, COUNT(), and GROUP BY to calculate the number of events associated with every user.

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

Results:

- sri – 2 events
- admin – 1 event
- john.doe – 1 event
- gabriel – 1 event
- test – 1 event
- eil – 1 event
- noah – 1 event
- temp_employee – 0 events

This provides an overview of recorded user activity.

### 5. Analyse Daily Failed Login Attempts

Used DATE() and GROUP BY to calculate failed login attempts by date.

```
SELECT
    DATE(ts) AS login_date,
    COUNT(*) AS failed_logins
FROM auth_logs
WHERE status = 'FAIL'
GROUP BY DATE(ts)
ORDER BY login_date;
```

Lab result:

- 2026-07-31 – 4 failed login attempts

This query helps identify dates with higher authentication failure activity.

### 6. Investigate Password Change Activities

Combined users and events tables using INNER JOIN to identify password-change events.

```
SELECT
    u.username,
    e.event_type,
    e.ts
FROM users u
JOIN events e
ON u.id = e.user_id
WHERE e.event_type = 'password_change';
```

The lab identified two password-change records:

- john.doe
- admin

This query helps review password-change activity associated with user accounts.

### 7. Investigate File Upload Activities

Used INNER JOIN to identify users associated with file-upload events.

```
SELECT
    u.username,
    e.event_type,
    e.ts
FROM users u
JOIN events e
ON u.id = e.user_id
WHERE e.event_type = 'file_upload';
```

The lab identified two file-upload records:

- sri
- gabriel

This helps investigate which accounts are associated with recorded file-upload activities.

## Security Monitoring Dashboard – Key Findings

| Security metric | Lab result |
|---|---:|
| Total user accounts | 8 |
| Users without recorded events | 1 |
| Total security events | 8 |
| Total authentication records | 6 |
| Failed authentication attempts | 4 |
| IP with the most failed attempts | 192.168.1.10 |
| Password-change events | 2 |
| File-upload events | 2 |

These results represent the sample lab dataset.

## Security Relevance

SQL-based security monitoring is useful in cloud security operations, SOC investigations, and database auditing.

These queries help security professionals:

- Identify IP addresses associated with repeated failed logins.
- Review recently created user accounts.
- Identify accounts without recorded security events.
- Monitor user activity patterns.
- Investigate password-change activities.
- Review file-upload activities.
- Analyse daily authentication failures.
- Prepare structured security monitoring reports.

**Security consideration:** Failed login attempts and unusual account activity are indicators for further investigation, not automatic proof of malicious activity.

## Screenshots

| Screenshot | Description |
|---|---|
| 01-failed-login-and-user-account-audit.png | Investigating failed logins, accounts without events, and recently created users |
| 02-user-activity-and-daily-login-analysis.png | Counting user events and analysing daily authentication failures |
| 03-password-change-and-file-upload-investigation.png | Investigating password-change and file-upload activities |

## Key Learning Outcomes

- Applying SQL to security monitoring.
- Analysing failed authentication attempts.
- Grouping login records by IP address.
- Identifying accounts without recorded events.
- Filtering recent user accounts using INTERVAL.
- Combining users and events using JOIN.
- Counting events using COUNT().
- Grouping records using GROUP BY.
- Analysing daily login failures using DATE().
- Investigating password-change events.
- Investigating file-upload activities.
- Preparing queries for security monitoring dashboards.

## Final Project Outcome

I completed a 20-day practical SQL learning project focused on cloud security monitoring and database investigations.

Applied PostgreSQL queries to investigate user accounts, authentication logs, failed login attempts, security events, and account activity.

Combined filtering, joins, subqueries, aggregate functions, database permissions, indexing, and relational database design to build practical SQL skills.

This project provides a foundation for entry-level Cloud Support, Cloud Security, SOC Analyst, and Security Operations opportunities.

---

**Project:** SQL for Cloud Security  
**Day:** 20  
**Status:** Completed  
**Milestone:** 20-Day SQL Practical Project Completed
