# Apply Filters to SQL Queries

**Josue Herrera**

## Project Description

In this project, I used SQL filtering techniques to investigate potential security issues within an organization's systems. By querying the `employees` and `log_in_attempts` tables, I retrieved and analyzed records related to employee activity and login events.
I applied SQL operators such as `AND`, `OR`, and `NOT` to filter data based on multiple conditions, identify suspicious login attempts, and examine employee machine information. Through these queries, I was able to isolate relevant records, support security investigations, and help identify potential threats or unauthorized access attempts within the organization.

---

## Tools Used

Throughout this project, I used the following tools and technologies:

- **SQL (Structured Query Language)** for querying and filtering data.
- **MySQL** for working with relational database tables and executing SQL statements.
- **Database Tables**
  - `log_in_attempts` table for investigating login activity and security events.
  - `employees` table for retrieving employee and departmental information.
- **SQL Operators**
  - `AND` to combine multiple conditions.
  - `OR` to retrieve records matching either condition.
  - `NOT` to exclude specific records.
  - `LIKE` to filter data using pattern matching.
- **Filtering Techniques** to identify relevant records for security investigations and system updates.

---

## Lessons Learned

Through this project, I strengthened my understanding of SQL filtering and its role in cybersecurity investigations. Some key lessons learned include:

- How to use the `WHERE` clause to filter database records efficiently.
- The importance of logical operators (`AND`, `OR`, and `NOT`) when narrowing down search results.
- How pattern matching with `LIKE` can be used to identify records based on partial values.
- The value of retrieving only relevant data when investigating security incidents.
- How SQL queries can support security monitoring, incident response, and audit activities.
- The importance of validating query results to ensure they accurately address the investigation requirements.
- How database filtering techniques can improve the efficiency and effectiveness of security operations.

---

## 1. Retrieve After-Hours Failed Login Attempts

My team was investigating failed login attempts made after business hours. Using my Maria's machine, I was asked to retrieve information about login activity that occurred after 18:00.

The `login_time` column in the `log_in_attempts` table contains information on when login attempts were made. Office hours end at `18:00`.

The `success` column contains Boolean values indicating whether a login was successful:

- `TRUE (1)` = Successful login
- `FALSE (0)` = Failed login

### SQL Query

```sql
SELECT *
FROM log_in_attempts
WHERE login_time > '18:00:00'
  AND success = 0;
```
<a href="//imgur.com/a/YD1822O">See image for step 1</a>

### Explanation

This query retrieves all login attempts that occurred after normal business hours (6:00 PM) and were unsuccessful.

The `AND` operator ensures that both conditions must be met:

- The login attempt occurred after 18:00.
- The login attempt failed (`success = 0`).

This information helps identify potentially suspicious login activity that may require further investigation.

---

## 2. Retrieve Login Attempts on Specific Dates

My team was investigating a suspicious event that occurred on `2022-05-09`. To support the investigation, I retrieved all login attempts that occurred on that day and the day before (`2022-05-08`).

The `login_date` column in the `log_in_attempts` table contains the dates of login attempts.

### SQL Query

```sql
SELECT *
FROM log_in_attempts
WHERE login_date = '2022-05-08'
   OR login_date = '2022-05-09';
```

<a href="//imgur.com/a/6rlbfQJ">See image for step 2</a>

### Explanation

This query returns all login attempts that occurred on either May 8, 2022, or May 9, 2022.

The `OR` operator is used because records from either date are relevant to the investigation.

Analyzing activity during these dates helps determine whether any unusual login behavior occurred around the time of the reported security event.

---

## 3. Retrieve Login Attempts Outside of Mexico

My team was investigating logins that did not originate from Mexico.

Since the `country` field includes values such as `MEX` and `MEXICO`, I used the matching pattern `MEX%`.

### SQL Query

```sql
SELECT *
FROM log_in_attempts
WHERE NOT country LIKE 'MEX%';
```
<a href="//imgur.com/a/rq5nC1y">See image for step 3</a>

### Explanation

This query identifies login attempts originating from locations outside Mexico.

The condition `LIKE 'MEX%'` matches entries beginning with `"MEX"`, including:

- `MEX`
- `MEXICO`

The `NOT` operator excludes these records, allowing the investigation to focus on login activity from other countries that may represent unauthorized access attempts.

---

## 4. Retrieve Employees in Marketing

My team continued auditing the `department` and `office` columns in the `employees` table.

### View Employee Records

```sql
SELECT *
FROM employees;
```

As part of a device update project, I needed information about employees in the **Marketing** department who worked in offices located in the **East** building.

### SQL Query

```sql
SELECT *
FROM employees
WHERE department = 'Marketing'
  AND office LIKE 'East%';
```
<a href="//imgur.com/a/uhIqdWO">See image for step 4</a>

### Explanation

This query retrieves employee records for individuals who work in the Marketing department and are located in offices within the East building.

The `AND` operator ensures that both conditions are satisfied, while `LIKE 'East%'` captures all office locations that begin with `"East"`.

This information was required to identify employee devices that needed updates.

---

## 5. Retrieve Employees in Finance or Sales

My team needed to perform a system update on the computers of employees in the **Finance** and **Sales** departments.

### SQL Query

```sql
SELECT *
FROM employees
WHERE department = 'Finance'
   OR department = 'Sales';
```
<a href="//imgur.com/a/pplHxiF">See image for step 5</a>

### Explanation

This query returns records for employees in either the Finance or Sales departments.

The `OR` operator allows records from both departments to be included in the results.

This information was used to identify employees whose computers required the update.

---

## 6. Retrieve All Employees Not in Information Technology

The Information Technology department had already received the required update, so my team needed information about employees outside of that department.

### SQL Query

```sql
SELECT *
FROM employees
WHERE NOT department = 'Information Technology';
```
<a href="//imgur.com/a/SjJEtcA">See images for step 6</a>

### Explanation

This query retrieves all employee records except those belonging to the Information Technology department.

The `NOT` operator excludes IT personnel because the required update had already been completed on their devices.

This allowed the team to focus on employees whose systems still needed updating.

---

# Summary

This project involved using SQL query filters to support a security investigation within an organization's database environment.

By analyzing data from the `employees` and `log_in_attempts` tables, I applied logical operators such as `AND`, `OR`, and `NOT` to:

- Identify suspicious login activity
- Investigate access attempts during specific timeframes
- Review login activity across multiple dates
- Examine access attempts from outside Mexico
- Retrieve employee information based on department and office location

These queries enabled efficient data analysis, supported security monitoring efforts, and contributed to maintaining the organization's overall security posture.
