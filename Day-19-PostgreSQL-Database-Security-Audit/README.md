# Day 19 – PostgreSQL Database Security Audit and Restore Verification

## Project Overview

This lab focuses on auditing a PostgreSQL database and verifying the integrity of restored database records.

The objective was to inspect user accounts, security events, and authentication logs in the restored database named `security_lab_restore`.

The lab demonstrates how SQL queries can be used to verify database records, review authentication activity, and perform basic post-restore validation.

## Environment

- Operating System: Ubuntu Linux
- Virtualisation: Oracle VirtualBox
- Database: PostgreSQL 17
- Database Name: `security_lab_restore`
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

### 1. Review Restored Security Event Records

Retrieved security event records from the restored database.

```
SELECT *
FROM events;
```

Reviewed the available event records, including:

- Login activities
- File uploads
- File downloads
- Password changes

The screenshot shows eight records in the events table.

### 2. Review Authentication Logs

Retrieved authentication records from the restored database.

```
SELECT *
FROM auth_logs;
```

Reviewed authentication information, including:

- Source IP addresses
- Authentication status
- Event timestamps
- Successful login attempts
- Failed login attempts

The screenshot shows six authentication records.

### 3. Verify Total User Accounts

Used COUNT() to calculate the number of user records.

```
SELECT COUNT(*)
FROM users;
```

**Result:** 8 user records.

### 4. Verify Total Security Events

Counted the security event records.

```
SELECT COUNT(*)
FROM events;
```

**Result:** 8 event records.

### 5. Verify Total Authentication Logs

Counted the authentication log records.

```
SELECT COUNT(*)
FROM auth_logs;
```

**Result:** 6 authentication records.

### 6. Review Authentication Status

Inspected the authentication logs to review successful and failed authentication attempts.

The dataset contains:

- SUCCESS: Successful authentication records.
- FAIL: Failed authentication records.

These records can help security professionals investigate authentication patterns and identify activity that requires further review.

## Database Audit Results

| Table | Verified record count |
|---|---:|
| users | 8 |
| events | 8 |
| auth_logs | 6 |
| Total | 22 |

The record counts were successfully retrieved from the restored database.

## Security Relevance

Database auditing and restore verification are important in cloud security operations and database administration.

These techniques help security professionals:

- Verify restored database records.
- Review user account information.
- Inspect security event records.
- Review authentication history.
- Identify successful and failed login attempts.
- Check database record counts.
- Support database integrity checks.
- Perform basic post-restore validation.

**Security consideration:** Matching record counts are a useful initial verification step, but they do not independently prove that a backup is complete or that every restored record is correct. Full validation should also include schema, constraints, indexes, permissions, and data comparisons.

## Screenshots

| Screenshot | Description |
|---|---|
| 01-restored-database-security-audit.png | Reviewing restored security events, authentication logs, and database record counts |

## Key Learning Outcomes

- Understanding database security auditing.
- Reviewing restored PostgreSQL databases.
- Retrieving security event records.
- Inspecting authentication logs.
- Counting database records using COUNT().
- Reviewing successful and failed authentication attempts.
- Performing basic post-restore verification.
- Understanding database integrity checks.
- Supporting database security investigations.

## Outcome

Successfully performed a basic PostgreSQL database security audit on the restored `security_lab_restore` database.

Verified 8 user records, 8 security event records, and 6 authentication log records.

Reviewed authentication statuses and security event information to understand basic database auditing and post-restore verification.

This lab provides a practical foundation in database administration, security auditing, and cloud security operations.

---

**Project:** SQL for Cloud Security  
**Day:** 19  
**Status:** Completed
