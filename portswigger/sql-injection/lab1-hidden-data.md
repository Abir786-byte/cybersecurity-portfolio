# Lab 1 — SQL Injection: Retrieving Hidden Data

**Platform:** PortSwigger Web Security Academy
**Difficulty:** Apprentice
**Status:** Solved

## Vulnerability
SQL Injection in WHERE clause

## Summary
The product category filter was vulnerable to SQL injection. By injecting into the category parameter, I retrieved hidden/unreleased products that normal users cannot see.

## Payload
```
' OR 1=1--
```

## Steps
1. Opened the shop and clicked a product category
2. Noticed URL parameter: `?category=Gifts`
3. Modified the value to: `Gifts' OR 1=1--`
4. All products including hidden ones appeared

## Why It Worked
The `--` comments out the rest of the query.
`OR 1=1` is always true, so all rows are returned regardless of conditions.

## Impact
Unauthorized access to hidden data — unreleased products exposed.

## Fix
Use parameterized queries (prepared statements).
