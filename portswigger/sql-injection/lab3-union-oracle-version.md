# Lab 3 — SQL Injection: Database Version on Oracle

**Platform:** PortSwigger Web Security Academy
**Difficulty:** Practitioner
**Status:** Solved

## Vulnerability
SQL Injection — UNION attack to retrieve database version

## Summary
Used UNION-based SQL injection to query the Oracle database version from the banner column.

## Payload
```
' UNION SELECT BANNER,NULL FROM v$version--
```

## Steps
1. Identified injection point in category parameter
2. Determined number of columns using ORDER BY
3. Found both columns return strings
4. Used UNION SELECT to query Oracle version table

## Key Oracle Notes
- Oracle requires `FROM` in every SELECT → use `FROM dual`
- Version info is in `v$version` table, column `BANNER`

## Impact
Database version disclosure — attacker can identify vulnerabilities specific to that version.

## Fix
Use parameterized queries. Never expose database errors to users.
