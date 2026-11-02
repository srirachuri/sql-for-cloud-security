# Day 14 – SQL HAVING Clause and Security Log Analysis

## Project Overview

This lab focuses on using the SQL HAVING clause to filter aggregated database records in PostgreSQL.

The objective was to investigate repeated failed login attempts, identify users with multiple security events, analyse event occurrences, and identify accounts with zero recorded activities.

The lab combines WHERE, GROUP BY, HAVING, COUNT(), LEFT JOIN, and ORDER BY to perform security log analysis.

## Environment

- Operating System: Ubuntu Linux
- Virtualisation: Oracle VirtualBox
- Database: PostgreSQL 17
- Database Name: `security_lab`
- Interface: PostgreSQL Command Line (psql)

## Database Tables

### Users Table
- id
- username
- email
- created_at

### Events Table
- id
- user_id
- event_type
- ts

### Authentication Logs Table
- id
- ip
- status
- ts

## Tasks Completed

### 1. Analyse Failed Login Attempts by IP Address

Used WHERE, GROUP BY, and COUNT() to calculate failed login attempts for each IP address.

```
SELECT
    ip,
    COUNT(*) AS failed_attempts
FROM auth_logs
WHERE status = 'FAIL'
GROUP BY ip;
```

Results:

- 192.168.1.10 – 2 failed attempts
- 172.16.0.15 – 1 failed attempt
- 192.168.1.01 – 1 failed attempt

### 2. Identify IP Addresses with More Than One Failed Login

Used HAVING to filter grouped authentication records.

```
SELECT
    ip,
    COUNT(*) AS failed_attempts
FROM auth_logs
WHERE status = 'FAIL'
GROUP BY ip
HAVING COUNT(*) > 1
ORDER BY failed_attempts DESC;
```

Result:

- 192.168.1.10 – 2 failed attempts

This helps identify IP addresses associated with repeated unsuccessful authentication attempts.

### 3. Filter IP Addresses with More Than Two Failed Attempts

Practised another HAVING condition.

```
SELECT
    ip,
    COUNT(*) AS failed_attempts
FROM auth_logs
WHERE status = 'FAIL'
GROUP BY ip
HAVING COUNT(*) > 2;
```

No matching records were returned because no IP address had more than two failed attempts in the dataset.

### 4. Identify Users with Multiple Security Events

Used GROUP BY and HAVING to identify users associated with more than one event.

```
SELECT
    user_id,
    COUNT(*) AS total_events
FROM events
GROUP BY user_id
HAVING COUNT(*) > 1;
```

Result:

- User ID 1 – 2 events

### 5. Identify Event Types with Multiple Occurrences

Grouped security events by event type and filtered for categories with more than one occurrence.

```
SELECT
    event_type,
    COUNT(*) AS occurrences
FROM events
GROUP BY event_type
HAVING COUNT(*) > 1;
```

Results:

- login – 3 occurrences
- file_upload – 2 occurrences
- password_change – 2 occurrences

### 6. Identify Users Without Recorded Events

Combined LEFT JOIN, GROUP BY, and HAVING to identify accounts without matching event records.

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

Result:

- temp_employee – 0 events

### 7. Identify Users with One or More Recorded Events

Used HAVING to retrieve users with at least one recorded security event.

```
SELECT
    u.username,
    COUNT(e.id) AS total_events
FROM users u
LEFT JOIN events e
ON u.id = e.user_id
GROUP BY u.username
HAVING COUNT(e.id) >= 1
ORDER BY total_events DESC;
```

The query returned seven users with recorded security events.

The results showed:

- sri – 2 events
- eil – 1 event
- test – 1 event
- noah – 1 event
- john.doe – 1 event
- gabriel – 1 event
- admin – 1 event

## Security Relevance

The HAVING clause is useful in cloud security monitoring, authentication analysis, and database investigations.

These techniques help security professionals:

- Identify IP addresses with repeated failed login attempts.
- Investigate users with multiple security events.
- Analyse frequently occurring event types.
- Identify accounts without recorded activities.
- Filter grouped authentication records.
- Detect patterns requiring further investigation.
- Summarise security logs using aggregate functions.

**Security consideration:** Repeated failed logins or unusual event counts are indicators for investigation, not automatic proof of malicious activity.

## Screenshots

| Screenshot | Description |
|---|---|
| 01-failed-login-analysis-by-ip.png | Grouping failed login attempts by IP address |
| 02-grouped-event-and-user-analysis.png | Filtering grouped results using HAVING |
| 03-users-with-zero-or-multiple-events.png | Identifying users with zero and multiple events |

## Key Learning Outcomes

- Understanding the SQL HAVING clause.
- Understanding WHERE versus HAVING.
- Filtering aggregated results.
- Combining WHERE and GROUP BY.
- Counting records using COUNT().
- Identifying repeated failed login attempts.
- Filtering event categories by occurrence count.
- Combining LEFT JOIN and HAVING.
- Identifying users without recorded events.
- Sorting aggregated results using ORDER BY.

## Outcome

Successfully practised advanced SQL aggregation and filtering using PostgreSQL.

Applied WHERE, GROUP BY, HAVING, COUNT(), LEFT JOIN, and ORDER BY to investigate authentication activity, identify repeated failed login attempts, and analyse user event patterns.

This lab provides practical foundations for security log analysis, database auditing, and cloud security monitoring.

---

**Project:** SQL for Cloud Security  
**Day:** 14  
**Status:** Completed
