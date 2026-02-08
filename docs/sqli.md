# SQL Injection

## Vulnerable pattern
String concatenation in SQL queries.

## Exploit
`' OR 1=1 --` to bypass auth.

## Fix
- Parameterized queries
- Input validation
- Least privilege DB user
