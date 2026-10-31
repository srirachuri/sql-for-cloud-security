# Day 8 – User Account and Activity Investigation Using SQL

## Project Overview

This lab focuses on investigating recently created user accounts, calculating account age, and analysing authentication activity using PostgreSQL.

The objective was to use SQL date and time functions, aggregate functions, and grouping operations to investigate account creation patterns and failed login attempts.

The lab also explores how SQL can help security professionals review recent user activity and identify authentication patterns that may require further investigation.

## Environment

- Operating System: Ubuntu Linux
- Virtualisation: Oracle VirtualBox
- Database: PostgreSQL 17
- Database Name: `security_lab`
- Interface: PostgreSQL Command Line (psql)

## Tasks Completed

### 1. Check Current Database Date

Used CURRENT_DATE to retrieve the current database date.

```
SELECT CURRENT_DATE;
```

### 2. Check Current Timestamp

Used CURRENT_TIMESTAMP to retrieve the current date and time.

```
SELECT CURRENT_TIMESTAMP;
```

### 3. Investigate Recently Created User Accounts

Retrieved user accounts created within the last 30 days.

```
SELECT id, username, email, created_at
FROM users
WHERE created_at >= CURRENT_DATE - INTERVAL '30 days'
ORDER BY created_at DESC;
```

This query displays recently created accounts, with the newest accounts appearing first.

### 4. Count Recently Created Accounts

Used COUNT() to calculate the number of accounts created within the last 30 days.

```
SELECT COUNT(*) AS recent_accounts
FROM users
WHERE created_at >= CURRENT_DATE - INTERVAL '30 days';
```

The query returned 6 recently created accounts in the lab dataset.

### 5. Calculate User Account Age

Used CURRENT_TIMESTAMP and timestamp subtraction to calculate how long each account has existed.

```
SELECT username,
       created_at,
       CURRENT_TIMESTAMP - created_at AS account_age
FROM users
ORDER BY created_at DESC;
```

This query displays account creation timestamps and their corresponding account ages.

### 6. Review Security Events from the Last 7 Days

Retrieved security events recorded within the previous seven days.

```
SELECT id, user_id, event_type, ts
FROM events
WHERE ts >= CURRENT_DATE - INTERVAL '7 days'
ORDER BY ts DESC;
```

Reviewed recorded activities such as:

- Login events
- File upload activities
- Password changes

### 7. Investigate Authentication Activity from the Last 24 Hours

Retrieved authentication records from the previous 24 hours.

```
SELECT id, ip, status, ts
FROM auth_logs
WHERE ts >= CURRENT_TIMESTAMP - INTERVAL '1 day'
ORDER BY ts DESC;
```

The query returned zero matching records in the lab dataset.

This demonstrates how time-based filtering can be used to investigate authentication activity within a specific period.

### 8. Count Failed Login Attempts by IP Address

Used COUNT() and GROUP BY to calculate failed authentication attempts for each IP address.

```
SELECT ip, COUNT(*) AS failed_attempts
FROM auth_logs
WHERE status = 'FAIL'
GROUP BY ip
ORDER BY failed_attempts DESC;
```

The query identified:

- IP address: `192.168.1.10`
- Failed login attempts: 2

This helps identify IP addresses associated with multiple failed authentication attempts.

## Security Relevance

User account and authentication analysis is important in cloud security monitoring and incident response.

These SQL techniques help security professionals:

- Identify recently created user accounts.
- Review account creation timelines.
- Calculate account age.
- Investigate recent user activities.
- Count failed authentication attempts.
- Identify IP addresses associated with repeated login failures.
- Review security events within specific time windows.
- Support database security audits.

**Note:** Multiple failed login attempts may indicate suspicious activity, but additional investigation is required before classifying an IP address as malicious.

## Screenshots

| Screenshot | Description |
|---|---|
| 01-current-date-and-recent-user-accounts.png | Checking database date and investigating recent accounts |
| 02-account-age-and-security-event-analysis.png | Calculating account age and reviewing security events |
| 03-failed-login-count-by-ip-address.png | Counting failed authentication attempts by IP address |

## Key Learning Outcomes

- Using CURRENT_DATE and CURRENT_TIMESTAMP.
- Filtering records using INTERVAL.
- Investigating recently created user accounts.
- Counting records using COUNT().
- Calculating account age using timestamp subtraction.
- Sorting records using ORDER BY.
- Reviewing recent security events.
- Grouping authentication records using GROUP BY.
- Identifying repeated failed login attempts by IP address.

## Outcome

Successfully performed user account and authentication activity investigations using PostgreSQL.

Applied date and time functions, aggregate functions, timestamp calculations, and grouping operations to analyse recent account creation, security events, and failed login activity.

This lab provides practical foundations for database auditing, security monitoring, and cloud security investigations.

---

**Project:** SQL for Cloud Security  
**Day:** 08  
**Status:** Completed
