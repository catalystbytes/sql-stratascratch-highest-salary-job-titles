# 🧑‍💼 SQL Case Study: Workers With The Highest Salaries

## 📌 Problem

Find the **job titles of employees with the highest salary**.

If multiple employees share the highest salary, include all their job titles.

Return:

* `best_paid_title`

---

## 🧠 Business Context

Management wants to analyze **top earners** in the company along with their roles.

This helps in:

* Compensation benchmarking
* Organizational analysis
* Identifying high-value roles

---

## 🗂️ Data Overview

### worker

| worker_id | first_name | last_name | salary | department |
| --------- | ---------- | --------- | ------ | ---------- |
| 3         | Vishal     | Singhal   | 300000 | HR         |
| 4         | Amitah     | Singh     | 500000 | Admin      |
| 5         | Vivek      | Bhati     | 500000 | Admin      |
| 13        | Jura       | Jomun     | 980000 | HR         |

---

### title

| worker_ref_id | worker_title  |
| ------------- | ------------- |
| 4             | Asst. Manager |
| 5             | Manager       |
| 3             | Lead          |

> Note: Data is truncated for readability.

---

## 🧩 Approach

### Step 1 — Identify Maximum Salary

* Use `MAX(salary)` from the `worker` table

### Step 2 — Join Tables

* Join `worker` with `title` to get job titles

### Step 3 — Filter

* Keep only employees whose salary equals the maximum

---


## 🧪 Solution

```sql
SELECT 
    b.worker_title AS best_paid_title
FROM worker a
JOIN title b 
    ON a.worker_id = b.worker_ref_id
WHERE a.salary = (
    SELECT MAX(w.salary)
    FROM worker w
    JOIN title t 
        ON t.worker_ref_id = w.worker_id
);
```


---

## ⚙️ Performance Considerations

* Subquery computes max salary once
* Avoid unnecessary joins inside subqueries
* Efficient for large datasets when indexed

---

## 🧠 Assumptions

* Each worker may have one or more titles
* Salary values are valid
* Highest salary uniquely defines top earners (ties allowed)

---

## 📊 Key Insights

* Subqueries are useful for scalar filtering
* JOIN + filter pattern is common in analytics
* Avoid redundant joins for better performance

---

## 📈 Business Takeaway

Identifying top earners and their roles helps:

* Understand compensation distribution
* Align salary structures
* Identify critical positions

---

## 🧪 Skills Demonstrated

* SQL JOIN
* Subquery (`MAX`)
* Filtering logic
* Query optimization
* Business interpretation

---

## ▶️ How to Use

1. Copy query into your SQL environment
2. Run against `worker` and `title` tables
3. Validate results

---

## 📌 Repository Structure

* `solution.sql` → initial implementation
* `insights.md` → summarized findings

---

## 🚀 Final Note

This project demonstrates how to:

* Combine multiple tables
* Use subqueries effectively
* Optimize SQL queries for real-world scenarios
