# Day 18 – PostgreSQL Normalisation and Data Types

## Project Overview

This lab focuses on PostgreSQL database structure, data types, relational database design, and security incident management.

The objective was to inspect existing database tables, understand PostgreSQL data types and constraints, create a dedicated security incidents table, establish a foreign key relationship with the users table, and insert a sample security incident.

The lab demonstrates how structured relational database design supports security incident tracking and database integrity.

## Environment

- Operating System: Ubuntu Linux
- Virtualisation: Oracle VirtualBox
- Database: PostgreSQL 17
- Database Name: `security_lab`
- Interface: PostgreSQL Command Line (psql)

## Tasks Completed

### 1. Inspect Existing Database Tables

Reviewed the structure of the users table.

```
\d users
```

Reviewed the events table.

```
\d events
```

Reviewed the authentication logs table.

```
\d auth_logs
```

Inspected column definitions, data types, primary keys, foreign keys, and existing indexes.

### 2. Understand PostgreSQL Data Types

Reviewed different PostgreSQL data types used in relational database design.

| Data type | Purpose |
|---|---|
| INTEGER | Stores whole numbers |
| SERIAL | Creates an auto-incrementing integer column |
| VARCHAR(150) | Stores variable-length text up to 150 characters |
| TEXT | Stores longer text descriptions |
| TIMESTAMP | Stores date and time values |

### 3. Create a Security Incidents Table

Created a dedicated table named `security_incidents` to store security incident information.

```
CREATE TABLE security_incidents (
    id SERIAL PRIMARY KEY,
    user_id INTEGER NOT NULL,
    incident_name VARCHAR(150) NOT NULL,
    severity INT NOT NULL,
    description TEXT,
    detected_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    FOREIGN KEY (user_id) REFERENCES users(id)
);
```

The table includes:

- `id`: Unique incident identifier.
- `user_id`: References the associated user account.
- `incident_name`: Name of the security incident.
- `severity`: Numerical severity value.
- `description`: Additional incident details.
- `detected_at`: Timestamp of incident creation.

### 4. Understand Primary Key Constraints

Used SERIAL and PRIMARY KEY to create a unique incident identifier.

```
id SERIAL PRIMARY KEY
```

This ensures that each incident record has a unique identifier.

### 5. Establish a Foreign Key Relationship

I connected the security incidents table to the users table.

```
FOREIGN KEY (user_id)
REFERENCES users(id)
```

This establishes a relationship between security incidents and existing user accounts.

The foreign key helps maintain referential integrity by preventing incident records from referencing nonexistent users.

### 6. Apply NOT NULL Constraints

Applied NOT NULL constraints to important columns.

```
user_id INTEGER NOT NULL,
incident_name VARCHAR(150) NOT NULL,
severity INT NOT NULL
```

These constraints ensure that essential incident information is provided when inserting records.

### 7. Set a Default Timestamp

Used CURRENT_TIMESTAMP to automatically populate the incident creation timestamp when a value is not explicitly provided.

```
detected_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
```

This helps maintain incident creation records without manually entering timestamps.

### 8. Insert a Security Incident

Inserted a sample brute-force attack incident into the new table.

```
INSERT INTO security_incidents
(user_id, incident_name, severity, description)
VALUES (
    1,
    'Brute Force Attack',
    5,
    'Multiple failed login attempts detected from 192.168.1.10'
);
```

The incident record included:

- User ID: 1
- Incident Name: Brute Force Attack
- Severity: 5
- Description: Multiple failed login attempts detected from 192.168.1.10

The detected_at timestamp was populated automatically.

### 9. Verify the Inserted Incident

Retrieved the inserted security incident record.

```
SELECT *
FROM security_incidents;
```

Verified that the incident was successfully inserted.

### 10. Inspect the Security Incidents Table

Used PostgreSQL's table description command to verify the new table structure.

```
\d security_incidents
```

Reviewed:

- Column names and data types.
- Primary key constraint.
- Foreign key constraint.
- NOT NULL constraints.
- Default timestamp value.

## Database Normalisation Concepts

Database normalisation helps organise relational data and reduce unnecessary duplication.

This lab demonstrates basic relational design principles:

### 1. Separate Related Information

User information remains in the users table, while incident-specific information is stored in the security_incidents table.

### 2. Establish Relationships

The user_id foreign key connects incident records to their corresponding user accounts.

### 3. Maintain Data Integrity

Primary keys, foreign keys, and NOT NULL constraints help maintain consistent database records.

**Note:** This exercise demonstrates relational table design and normalisation principles. A complete normalisation assessment would require checking functional dependencies and verifying the relevant normal forms.

## Security Relevance

Database design and normalisation are important in cloud security monitoring and incident management.

These techniques help security professionals:

- Maintain structured security incident records.
- Associate incidents with user accounts.
- Maintain referential integrity.
- Store incident descriptions and severity values.
- Record incident timestamps automatically.
- Reduce unnecessary duplication of user information.
- Build a foundation for incident investigation and reporting.

## Screenshots

| Screenshot | Description |
|---|---|
| 01-existing-database-table-structures.png | Inspecting users, events, and authentication log tables |
| 02-security-incident-table-creation.png | Creating the security incidents table and defining constraints |
| 03-incident-record-insertion-and-verification.png | Inserting and verifying a brute-force attack incident |

## Key Learning Outcomes

- Understanding PostgreSQL data types.
- Inspecting database table structures.
- Understanding relational database design.
- Learning basic normalisation principles.
- Creating tables using CREATE TABLE.
- Defining primary key constraints.
- Establishing foreign key relationships.
- Applying NOT NULL constraints.
- Using DEFAULT CURRENT_TIMESTAMP.
- Inserting security incident records.
- Verifying database structure and records.

## Outcome

Successfully designed and created a PostgreSQL security incidents table.

Applied data types, primary keys, foreign keys, NOT NULL constraints, and default timestamps to build a structured incident management table.

Inserted and verified a sample brute-force attack incident.

This lab provides practical foundations for relational database design, security incident tracking, and cloud security operations.

---

**Project:** SQL for Cloud Security  
**Day:** 18  
**Status:** Completed
