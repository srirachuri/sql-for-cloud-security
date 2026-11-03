# SQL for Cloud Security – 20-Day Practical Project

![PostgreSQL](https://img.shields.io/badge/Database-PostgreSQL-4169E1?logo=postgresql&logoColor=white)
![SQL](https://img.shields.io/badge/Language-SQL-orange)
![Security](https://img.shields.io/badge/Focus-Cloud%20Security-red)
![Status](https://img.shields.io/badge/Project-Completed-success)

## Project Overview

This repository contains a 20-day hands-on SQL learning project focused on PostgreSQL, database administration, security monitoring, and user activity investigations.

The project was designed to develop practical SQL skills relevant to Cloud Support, Cloud Security, Security Operations Centre (SOC), and Junior Cloud Security roles.

Throughout this project, I worked with user account records, authentication logs, security events, database permissions, and security incident records.

The final objective was to develop SQL queries that can support security monitoring and investigation workflows.

## Technologies and Tools

| Technology | Purpose |
|---|---|
| PostgreSQL 17 | Relational database management |
| SQL | Database querying and analysis |
| Ubuntu Linux | Operating environment |
| Oracle VirtualBox | Virtualization |
| pgSQL / psql | PostgreSQL command-line interface |
| GitHub | Project documentation and version control |

## Project Structure

```
sql-for-cloud-security/
│
├── Day-01-PostgreSQL-Setup/
├── Day-02-SQL-SELECT-Basics/
├── Day-03-Employee-Account-Lookup/
├── Day-04-SQL-Filtering-and-Pattern-Matching/
├── Day-05-Suspicious-Login-Investigation/
├── Day-06-Recent-Login-Activity-Analysis/
├── Day-07-SQL-Date-and-Time-Analysis/
├── Day-08-User-Account-Activity-Investigation/
├── Day-09-SQL-Data-Manipulation-and-Transactions/
├── Day-10-SQL-INNER-JOIN-Security-Log-Analysis/
├── Day-11-SQL-LEFT-JOIN-User-Activity-Analysis/
├── Day-12-SQL-RIGHT-JOIN-User-Activity-Analysis/
├── Day-13-SQL-GROUP-BY-and-Aggregation/
├── Day-14-SQL-HAVING-Clause-Security-Analysis/
├── Day-15-SQL-Subqueries-User-Activity-Analysis/
├── Day-16-SQL-EXISTS-and-NOT-EXISTS/
├── Day-17-PostgreSQL-Indexes-and-RBAC/
├── Day-18-PostgreSQL-Normalization-and-Data-Types/
├── Day-19-PostgreSQL-Database-Security-Audit/
├── Day-20-SQL-Security-Dashboard-Queries/
│
└── README.md
```

Each daily folder contains a README.md explaining the exercises and a screenshots folder containing practical lab evidence.

## 20-Day Learning Roadmap

| Day | Topic | Skills Practised |
|---|---|---|
| 01 | PostgreSQL Setup | Installation and database configuration |
| 02 | SELECT Basics | Retrieving database records |
| 03 | Employee Account Lookup | User account investigation |
| 04 | Filtering and Pattern Matching | WHERE, LIKE, AND, OR |
| 05 | Suspicious Login Investigation | Comparison operators and authentication analysis |
| 06 | Recent Login Activity | ORDER BY and LIMIT |
| 07 | Date and Time Analysis | CURRENT_DATE, timestamps, INTERVAL |
| 08 | Recent User Accounts | Account age and time-based filtering |
| 09 | Data Manipulation | INSERT, UPDATE, DELETE, transactions |
| 10 | INNER JOIN | User and security event correlation |
| 11 | LEFT JOIN | Identifying users without matching events |
| 12 | RIGHT JOIN | Relational database investigation |
| 13 | GROUP BY and Aggregation | COUNT, SUM, AVG |
| 14 | HAVING | Filtering aggregated security records |
| 15 | Subqueries | IN and NOT IN |
| 16 | EXISTS and NOT EXISTS | Correlated subqueries |
| 17 | Indexes and RBAC | Query performance and database permissions |
| 18 | Normalization and Data Types | Relational database design |
| 19 | Database Security Audit | Restore verification and record validation |
| 20 | Security Dashboard Queries | Security monitoring and investigation |

## Database Schema

The practical exercises use three primary database tables and one additional incident management table.

### 1. Users

Stores user account information.

- id
- username
- email
- created_at

### 2. Events

Stores user activity and security event information.

- id
- user_id
- event_type
- ts

### 3. Authentication Logs

Stores authentication activity.

- id
- ip
- status
- ts

### 4. Security Incidents

Stores security incident information.

- id
- user_id
- incident_name
- severity
- description
- detected_at

## Key SQL Skills Demonstrated

### Database Querying
- SELECT
- WHERE
- ORDER BY
- LIMIT
- DISTINCT
- LIKE
- AND / OR

### Date and Time Analysis
- CURRENT_DATE
- CURRENT_TIMESTAMP
- INTERVAL
- Timestamp calculations
- DATE()

### Data Manipulation
- INSERT
- UPDATE
- DELETE
- BEGIN
- COMMIT
- ROLLBACK

### Relational Database Operations
- INNER JOIN
- LEFT JOIN
- RIGHT JOIN
- GROUP BY
- HAVING
- COUNT()
- SUM()
- AVG()

### Advanced SQL
- Subqueries
- IN
- NOT IN
- EXISTS
- NOT EXISTS
- Correlated subqueries

### Database Security and Administration
- CREATE INDEX
- EXPLAIN
- CREATE USER
- GRANT
- REVOKE
- Primary keys
- Foreign keys
- NOT NULL constraints
- Database normalisation

## Practical Security Investigations

The project includes practical SQL investigations such as:

1. Identifying IP addresses associated with repeated failed login attempts.
2. Investigating user accounts with suspicious authentication patterns.
3. Identifying accounts without recorded security events.
4. Reviewing recently created user accounts.
5. Investigating password-change activities.
6. Identifying users associated with file uploads.
7. Counting security events by user.
8. Analysing successful and failed authentication attempts.
9. Reviewing database permissions and least-privilege access.
10. Verifying restored database records.

## Final Project – Security Monitoring Queries

The final day combines multiple SQL concepts to prepare queries for a security monitoring dashboard.

Example: Identifying IP addresses with repeated failed authentication attempts.

```
SELECT
    ip,
    COUNT(*) AS failed_attempts
FROM auth_logs
WHERE status = 'FAIL'
GROUP BY ip
ORDER BY failed_attempts DESC;
```

Example: Identifying users without recorded security events.

```
SELECT
    u.username,
    u.email
FROM users u
LEFT JOIN events e
ON u.id = e.user_id
WHERE e.id IS NULL;
```

Example: Investigating password-change activities.

```
SELECT
    u.username,
    e.event_type,
    e.ts
FROM users u
INNER JOIN events e
ON u.id = e.user_id
WHERE e.event_type = 'password_change';
```

These queries demonstrate how SQL can support security monitoring, account auditing, and incident investigation.

## Key Learning Outcomes

By completing this 20-day practical project, I developed hands-on experience in:

- PostgreSQL database management.
- SQL querying and filtering.
- User account investigations.
- Authentication log analysis.
- Security event correlation.
- Relational database operations.
- Aggregate functions and subqueries.
- Database indexing and query execution plans.
- Role-Based Access Control (RBAC).
- Database normalisation and constraints.
- Security incident record management.
- Basic database auditing and restore verification.

## Future Improvements

Planned improvements to this project include:

- Building Python scripts for automated security log analysis.
- Connecting PostgreSQL with Python.
- Automating suspicious login detection.
- Creating a security monitoring dashboard.
- Integrating SQL investigations with cloud security monitoring workflows.
- Exploring AWS and Azure security log analysis.

## Project Information

| Detail | Information |
|---|---|
| Project | SQL for Cloud Security |
| Duration | 20 Days |
| Database | PostgreSQL 17 |
| Environment | Ubuntu Linux |
| Virtualization | Oracle VirtualBox |
| Documentation | GitHub |
| Status | Completed |

## Author

**Sri Gayathri Rachuri**

Aspiring Cloud Security Professional

Interested in Cloud Security, PostgreSQL, Security Operations, AWS, Azure, and Security Automation.

---

*This repository documents my hands-on learning journey in SQL and its practical applications in cloud security monitoring and database investigations.*
