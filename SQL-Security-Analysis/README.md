# SQL Security Analysis Project

**Investigating Login Activity & Employee Machines**

---

## About This Project

As part of my cybersecurity journey, I'm building hands-on portfolio projects to demonstrate the skills I'm developing. This project showcases my ability to use SQL for security investigations.

In this analysis, I examined login attempts and employee metadata to detect anomalies, suspicious activity, and patterns that would be relevant in real-world incident response scenarios.

---

## What I Investigated

I worked with two organizational database tables:

- `employees`
- `log_in_attempts`

My analysis included:

- Identifying failed after-hours logins
- Investigating suspicious date-based login patterns
- Filtering logins by geographic indicators
- Locating employees by department and building
- Identifying users outside IT requiring system updates
- Applying SQL operators such as `AND`, `OR`, `LIKE`, and `NOT`

---

## My SQL Analysis Process

### Step 1: Finding After-Hours Failed Login Attempts

**My Goal:** Identify failed login attempts after 18:00.

**Query I Used:**
```sql
SELECT *
FROM log_in_attempts
WHERE login_time > '18:00'
  AND success = 0;
```

**My Approach:**

- I filtered for `login_time > '18:00'` to catch attempts after business hours
- I used `success = 0` to select only failed attempts
- The `AND` operator ensured both conditions were met

**What I Found:** 19 failed login attempts occurred after hours.

**Query Results:**
![After-hours failed login attempts](Screenshot%202025-11-16%20160756.png)

---

### Step 2: Investigating Login Attempts on Specific Dates

**My Goal:** Review activity on 2022-05-09 and the day before.

**Query I Used:**
```sql
SELECT *
FROM log_in_attempts
WHERE login_date = '2022-05-08'
   OR login_date = '2022-05-09';
```

**My Approach:**

- I used `OR` to return rows matching either date
- I enclosed dates in quotes for proper SQL syntax
- This is useful when investigating events surrounding a specific incident

**What I Found:** 75 login attempts occurred across both days.

**Query Results:**
![Investigating Login Attempts on Specific Dates1](Screenshot%2025-11-16%160824.png)
![Investigating Login Attempts on Specific Dates2](Screenshot%2025-11-16%160832.png)

---

### Step 3: Identifying Login Attempts Outside Mexico

**My Goal:** Find login attempts originating from outside Mexico.

**Query I Used:**
```sql
SELECT *
FROM log_in_attempts
WHERE NOT country LIKE 'MEX%';
```

**My Approach:**

- I used `LIKE 'MEX%'` to match both MEX and MEXICO
- The `NOT` operator excluded all Mexico-based attempts
- The `%` wildcard matched any trailing characters

**What I Found:** 144 login attempts originated outside Mexico.

**Query Results:**
![Investigating Login Attempts on Specific Dates2](Screenshot%2025-11-16%160856.png)
![Investigating Login Attempts on Specific Dates2](Screenshot%2025-11-16%160904.png)

---

### Step 4: Locating Marketing Employees in East Building

**My Goal:** Identify Marketing employees in the East building for targeted updates.

**Query I Used:**
```sql
SELECT *
FROM employees
WHERE department = 'Marketing'
  AND office LIKE 'East%';
```

**My Approach:**

- I filtered for `department = Marketing`
- I used `office LIKE 'East%'` to match the office prefix
- The `AND` operator ensured both conditions matched

**What I Found:** 7 employees met the criteria, starting with elarson.

**Query Results:**
![Investigating Login Attempts on Specific Dates2](Screenshot%2025-11-16%160932.png)

---

### Step 5: Compiling Finance and Sales Employees

**My Goal:** Get a list of all employees in Finance or Sales departments.

**Query I Used:**
```sql
SELECT *
FROM employees
WHERE department = 'Finance'
   OR department = 'Sales';
```

**My Approach:**

- I used `OR` to include both departments
- I made sure to reference the department column for each condition
- This is useful for bulk system updates

**What I Found:** Multiple employees from both departments, including lrodriqu.

**Query Results:**
![Investigating Login Attempts on Specific Dates2](Screenshot%2025-11-16%160955.png)


---

### Step 6: Finding All Employees Outside IT

**My Goal:** Identify employees needing updates, excluding IT staff who were already patched.

**Query I Used:**
```sql
SELECT *
FROM employees
WHERE NOT department = 'Information Technology';
```

**My Approach:**

- I used `NOT` to exclude all IT department employees
- This returned all remaining departments
- Helpful for targeted patching and compliance tasks

**What I Found:** 161 employees outside the IT department needed updates.

**Query Results:**
![Investigating Login Attempts on Specific Dates2](Screenshot%2025-11-16%161018.png)
![Investigating Login Attempts on Specific Dates2](Screenshot%2025-11-16%161024.png)

---

## Skills I Demonstrated

**SQL Techniques:**
- Comparison operators: `>`, `<`, `=`, `<>`, `>=`, `<=`
- Time and date filtering
- Wildcard filtering using `LIKE` and `%`
- Logical operators: `AND`, `OR`, `NOT`

**Security Analysis:**
- Identifying failed login patterns
- Reviewing suspicious timeframes
- Geographic activity analysis
- Department and location-based filtering

---

## What I Learned

Through this project, I strengthened my ability to:

- Write efficient SQL queries for security investigations
- Use logical operators to combine multiple conditions
- Apply pattern matching for flexible data filtering
- Analyze login data to identify potential security threats
- Extract actionable insights from large datasets

These techniques mirror real-world scenarios that cybersecurity analysts face when processing data to detect threats, ensure compliance, and respond to incidents.

---

## Tools & Technologies

- SQL (Structured Query Language)
- Database querying and filtering
- Security analysis methodology
