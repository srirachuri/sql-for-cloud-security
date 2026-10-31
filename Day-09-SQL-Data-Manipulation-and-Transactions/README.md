# Day 9 – SQL Data Manipulation and Transaction Management

## Project Overview

This lab focuses on managing user account records using SQL Data Manipulation Language (DML) commands in PostgreSQL.

The objective was to practise inserting new user records, updating existing account information, deleting selected records, and managing database transactions using BEGIN, COMMIT, and ROLLBACK.

The lab demonstrates how database administrators and security professionals can manage user information while maintaining data integrity.

## Environment

- Operating System: Ubuntu Linux
- Virtualisation: Oracle VirtualBox
- Database: PostgreSQL 17
- Database Name: `security_lab`
- Interface: PostgreSQL Command Line (psql)

## Tasks Completed

### 1. Insert New User Records

Used INSERT INTO to add a new employee account to the users table.

```
INSERT INTO users (username, email)
VALUES ('john_doe', 'john.doe@company.com');
```

Verified the inserted record.

```
SELECT *
FROM users
WHERE username = 'john_doe';
```

### 2. Update Existing User Information

Used UPDATE to modify an existing employee's email address.

```
UPDATE users
SET email = 'new.email@company.com'
WHERE id = 2;
```

Verified the updated record.

```
SELECT *
FROM users
WHERE id = 2;
```

The WHERE condition ensures that only the selected user record is updated.

### 3. Manage Transactions Using BEGIN

I started a database transaction before making changes.

```
BEGIN;
```

Updated a temporary user account.

```
UPDATE users
SET email = 'temporary@company.com'
WHERE id = 7;
```

Verified the change before completing the transaction.

```
SELECT *
FROM users
WHERE id = 7;
```

### 4. Roll Back Database Changes

Used ROLLBACK to reverse the uncommitted transaction.

```
ROLLBACK;
```

Verified that the temporary change was reversed.

This demonstrated how transactions can protect database records from unintended modifications.

### 5. Delete Selected User Records

Used DELETE FROM to remove a selected user record.

```
DELETE FROM users
WHERE email = 'suspicious@company.com';
```

Verified the deletion.

```
SELECT *
FROM users
WHERE email = 'suspicious@company.com';
```

The query returned no matching records after deletion.

**Important:** Always verify the WHERE condition with a SELECT query before executing DELETE in a real database.

### 6. Count User Records

Used COUNT() to calculate the total number of user records.

```
SELECT COUNT(*) AS total_users
FROM users;
```

This helped verify the number of records remaining in the users table.

### 7. Review User Records

Retrieved selected user information and sorted records by ID.

```
SELECT id, username, email, created_at
FROM users
ORDER BY id;
```

Reviewed the resulting records to verify database changes.

## Security Relevance

Data manipulation and transaction management are important in database administration and cloud security operations.

These techniques help professionals:

- Create and manage user account records.
- Update incorrect account information.
- Remove unwanted database records.
- Protect data integrity using transactions.
- Reverse uncommitted changes.
- Verify database modifications.
- Reduce accidental changes through careful use of WHERE conditions.

**Security best practice:** Use least-privilege database permissions, review changes before execution, and maintain appropriate backups and audit logs.

## Screenshots

| Screenshot | Description |
|---|---|
| 01-insert-user-records.png | Inserting and verifying new user records |
| 02-update-and-transaction-rollback.png | Updating user information and testing ROLLBACK |
| 03-delete-and-verify-user-records.png | Deleting selected records and verifying results |
| 04-transaction-and-record-count-verification.png | Reviewing deletion results and counting records |

## Key Learning Outcomes

- Understanding SQL Data Manipulation Language (DML).
- Inserting records using INSERT INTO.
- Updating records using UPDATE.
- Deleting records using DELETE.
- Filtering modifications using WHERE.
- Managing transactions using BEGIN.
- Understanding COMMIT and ROLLBACK.
- Verifying database modifications using SELECT.
- Counting database records using COUNT().
- Maintaining database integrity.

## Outcome

Successfully practised SQL data manipulation and transaction management using PostgreSQL.

Applied INSERT, UPDATE, DELETE, BEGIN, and ROLLBACK to manage user account records and understand how database transactions help protect data integrity.

This lab provides a foundation for secure database administration, access management, and cloud security operations.

---

**Project:** SQL for Cloud Security  
**Day:** 09  
**Status:** Completed
