# Lab 2 — SQL Injection: Login Bypass

**Platform:** PortSwigger Web Security Academy
**Difficulty:** Apprentice
**Status:** Solved

## Vulnerability
SQL Injection in login form

## Summary
The login form was vulnerable to SQL injection. By injecting into the username field, I bypassed authentication and logged in as administrator without knowing the password.

## Payload
```
Username: administrator'--
Password: anything
```

## Steps
1. Opened the login page
2. Entered `administrator'--` as username
3. Entered any random string as password
4. Successfully logged in as administrator

## Why It Worked
Backend query:
```sql
SELECT * FROM users WHERE username='administrator'--' AND password='anything'
```
The `--` comments out the password check entirely.

## Impact
Complete authentication bypass — full admin access without credentials.

## Fix
Use parameterized queries. Never concatenate user input into SQL queries.
