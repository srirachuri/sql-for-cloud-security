# Day 17 – PostgreSQL Indexes and Role-Based Access Control (RBAC)

## Project Overview

This lab focuses on PostgreSQL database performance optimisation and access control management.

The objective was to create indexes on frequently queried database columns, inspect query execution plans using EXPLAIN, create a database role for a SOC analyst, and manage database permissions using GRANT and REVOKE.

The lab demonstrates how database administrators and security professionals can improve query performance while enforcing least-privilege access control.

## Environment

- Operating System: Ubuntu Linux
- Virtualisation: Oracle VirtualBox
- Database: PostgreSQL 17
- Database Name: `security_lab`
- Interface: PostgreSQL Command Line (psql)

## Tasks Completed

### 1. Review Authentication Logs

Retrieved authentication records associated with a specific IP address.

```
SELECT *
FROM auth_logs
WHERE ip = '192.168.1.10';
```

Reviewed failed authentication records associated with the selected IP address.

### 2. Create an Index on Authentication Logs

Created an index on the IP address column in the authentication logs table.

```
CREATE INDEX idx_auth_logs_ip
ON auth_logs(ip);
```

This index can help improve queries that search authentication records by IP address.

### 3. Inspect Query Execution Using EXPLAIN

Used EXPLAIN to inspect the execution plan for an IP-based authentication query.

```
EXPLAIN
SELECT *
FROM auth_logs
WHERE ip = '192.168.1.10';
```

The execution plan showed a sequential scan on the small authentication log table.

This demonstrates that PostgreSQL's query optimiser may choose a sequential scan instead of an index scan when it considers that approach more efficient.

### 4. Create an Index on Events

Created an index on the user_id column in the events table.

```
CREATE INDEX idx_events_user_id
ON events(user_id);
```

This index can help queries that retrieve security events associated with individual users.

### 5. Create an Index on User Email

Created an index on the email column in the users table.

```
CREATE INDEX idx_users_email
ON users(email);
```

This can improve lookups that search for users by email address.

### 6. Verify Database Indexes

Used PostgreSQL system catalogue information to inspect indexes on the authentication logs table.

```
SELECT indexname, tablename
FROM pg_indexes
WHERE tablename = 'auth_logs';
```

The lab verified the following indexes:

- auth_logs_pkey
- idx_auth_logs_ip

### 7. Create a SOC Analyst Database Role

Created a PostgreSQL role named `soc_analyst` with login access.

```
CREATE USER soc_analyst
WITH PASSWORD '<YOUR_SECURE_PASSWORD>';
```

A secure password should be supplied locally and never committed to GitHub.

### 8. Grant Database Connection Permission

I granted permission to connect to the security database.

```
GRANT CONNECT
ON DATABASE security_lab
TO soc_analyst;
```

This allows the role to connect to the specified database.

### 9. Grant Schema Usage Permission

Granted usage permission on the public schema.

```
GRANT USAGE
ON SCHEMA public
TO soc_analyst;
```

This allows the role to access objects in the schema when the necessary object permissions are also granted.

### 10. Grant SELECT Permissions

Granted read access to all existing tables in the public schema.

```
GRANT SELECT
ON ALL TABLES IN SCHEMA public
TO soc_analyst;
```

This allows the SOC analyst role to retrieve database records without automatically receiving modification permissions.

### 11. Revoke Modification Permissions

Revoked INSERT, UPDATE, and DELETE permissions from the SOC analyst role on all tables in the public schema.

```
REVOKE INSERT, UPDATE, DELETE
ON ALL TABLES IN SCHEMA public
FROM soc_analyst;
```

This follows the principle of least privilege by restricting unnecessary database modifications.

### 12. Test INSERT Permission

Temporarily granted INSERT permission on the authentication logs table.

```
GRANT INSERT
ON auth_logs
TO soc_analyst;
```

Then revoked the permission.

```
REVOKE INSERT
ON auth_logs
FROM soc_analyst;
```

This demonstrated how database permissions can be granted and revoked for specific tables.

### 13. Remove the Temporary SOC Analyst Role

Removed ownership and deleted the temporary role after completing the access-control exercise.

```
DROP OWNED BY soc_analyst;

DROP USER soc_analyst;
```

The role was removed after the permission-management exercise.

## Security Relevance

Database indexing and RBAC are important in cloud security, database administration, and security operations.

These techniques help security professionals:

- Improve database lookup performance.
- Investigate authentication records efficiently.
- Inspect SQL query execution plans.
- Manage database user roles.
- Enforce least-privilege access.
- Grant read-only database access.
- Restrict unauthorised data modifications.
- Control INSERT, UPDATE, and DELETE permissions.
- Reduce unnecessary database privileges.

**Security best practices:**

- Use strong, unique passwords.
- Never publish database passwords in GitHub repositories.
- Grant only the permissions required for a user's responsibilities.
- Review database permissions regularly.
- Monitor database activity and audit privilege changes.
- Evaluate index performance before adding indexes to production databases.

## Screenshots

| Screenshot | Description |
|---|---|
| 01-authentication-log-index-and-explain.png | Creating an authentication log index and inspecting the execution plan |
| 02-user-event-indexes-and-role-creation.png | Creating user and event indexes and configuring the SOC analyst role |
| 03-soc-analyst-permissions-and-role-management.png | Managing GRANT, REVOKE, and role removal |

## Key Learning Outcomes

- Understanding PostgreSQL indexes.
- Creating indexes using CREATE INDEX.
- Improving database lookup performance.
- Inspecting query plans using EXPLAIN.
- Understanding sequential scans and index scans.
- Reviewing PostgreSQL index information.
- Creating database roles and users.
- Managing database permissions using GRANT.
- Revoking permissions using REVOKE.
- Implementing least-privilege access control.
- Managing temporary database roles.

## Outcome

Successfully practised PostgreSQL indexing and Role-Based Access Control.

Created indexes on authentication logs, user IDs, and email addresses. Inspected query execution plans and configured a temporary SOC analyst role with controlled database permissions.

This lab provides practical foundations for database performance optimisation, access management, and cloud security operations.

---

**Project:** SQL for Cloud Security  
**Day:** 17  
**Status:** Completed
