# Day 7 – SQL Date and Time Analysis

## Project Overview

This lab focuses on analysing user activity, authentication records, and security events using SQL date and time functions in PostgreSQL.

The objective was to investigate recent login attempts, filter records within specific time periods, identify recently created accounts, and review password-change events.

PostgreSQL date and time functions, including CURRENT_DATE, NOW(), and INTERVAL, were used to perform time-based security investigations.

## Environment

- Operating System: Ubuntu Linux
- Virtualisation: Oracle VirtualBox
- Database: PostgreSQL 17
- Database Name: `security_lab`
- Interface: PostgreSQL Command Line (psql)

## Tasks Completed

### 1. Retrieve Recently Created User Accounts

Used CURRENT_DATE and INTERVAL to retrieve user accounts created within the last 30 days.

```
SELECT *
FROM users
WHERE created_at >= CURRENT_DATE - INTERVAL '30 days';
```

This query helps review recently created user accounts.

### 2. Analyse Authentication Logs from the Last 7 Days

Filtered authentication records using a seven-day time period.

```
SELECT *
FROM auth_logs
WHERE ts >= CURRENT_DATE - INTERVAL '7 days';
```

Reviewed successful and failed authentication records within the selected period.

### 3. Investigate Failed Login Attempts from the Last 24 Hours

Used NOW() and INTERVAL to identify recent failed authentication attempts.

```
SELECT *
FROM auth_logs
WHERE status = 'FAIL'
AND ts >= NOW() - INTERVAL '24 hours';
```

This query retrieves failed login attempts recorded within the previous 24 hours.

### 4. Investigate Security Events from the Last 48 Hours

Filtered event records using a 48-hour time window.

```
SELECT *
FROM events
WHERE ts >= NOW() - INTERVAL '48 hours';
```

Reviewed recorded user activities, including:

- Login events
- File upload activities
- Password changes

### 5. Investigate Recent Password Changes

Filtered the events table to identify password-change activities within the last seven days.

```
SELECT *
FROM events
WHERE event_type = 'password_change'
AND ts >= CURRENT_DATE - INTERVAL '7 days';
```

This helps review recent password-related activities.

### 6. Analyse Failed Login Attempts from the Last 30 Days

Retrieved failed authentication records and sorted them by timestamp in descending order.

```
SELECT *
FROM auth_logs
WHERE status = 'FAIL'
AND ts >= CURRENT_DATE - INTERVAL '30 days'
ORDER BY ts DESC;
```

This query displays the most recent failed authentication records first.

### 7. Check User Accounts Created Today

Used CURRENT_DATE to filter accounts created on or after the beginning of the current date.

```
SELECT *
FROM users
WHERE created_at >= CURRENT_DATE;
```

The query returned zero records in this lab, indicating that no matching accounts were found for the selected date.

## Security Relevance

Date and time analysis is important in cloud security monitoring, SOC operations, and incident response.

These techniques help security professionals:

- Investigate recent authentication attempts.
- Identify failed logins within specific time windows.
- Review newly created user accounts.
- Investigate recent password changes.
- Analyse security events using timestamps.
- Establish timelines during incident investigations.
- Narrow down relevant records during security audits.

## Screenshots

| Screenshot | Description |
|---|---|
| 01-date-based-user-and-login-filtering.png | Filtering user and authentication records using date conditions |
| 02-recent-security-event-analysis.png | Investigating recent security events and failed logins |

## Key Learning Outcomes

- Understanding PostgreSQL date and time functions.
- Using CURRENT_DATE.
- Using NOW().
- Working with INTERVAL values.
- Filtering records by date and timestamp.
- Investigating authentication activity within 24-hour, 7-day, and 30-day periods.
- Reviewing security events within 48 hours.
- Investigating password-change activities.
- Sorting time-based security records.

## Outcome

Successfully practised SQL date and time analysis using PostgreSQL.

Applied CURRENT_DATE, NOW(), INTERVAL, WHERE, and ORDER BY to investigate authentication records, user account creation, and recent security events.

This lab provides a foundation for time-based security monitoring, authentication investigations, and incident response.

---

**Project:** SQL for Cloud Security  
**Day:** 07  
**Status:** Completed
