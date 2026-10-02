# Lab 4 — SQL Injection: Database Version on MySQL and Microsoft

**Platform:** PortSwigger Web Security Academy
**Difficulty:** Practitioner
**Status:** Solved

## Vulnerability
SQL Injection — UNION attack to retrieve database version

## Summary
Used UNION-based SQL injection to retrieve database version on MySQL/Microsoft SQL Server.

## Payload
```
' UNION SELECT @@version,NULL-- -
```

## Steps
1. Identified injection point in category parameter
2. Determined column count with ORDER BY
3. Used `@@version` to get database version
4. Note: MySQL comments need `-- -` (space after --)

## Key MySQL/MSSQL Notes
- Version variable: `@@version`
- Comment syntax: `-- -` or `#`
- No need for FROM clause (unlike Oracle)

## Impact
Database version disclosure — helps attacker identify exploitable vulnerabilities.

## Fix
Use parameterized queries. Disable verbose error messages in production.
