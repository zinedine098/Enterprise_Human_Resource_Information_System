# 🧱 1️⃣ Users & Roles

---

## 📌 `roles`

| Column     | Type        | Constraint |
| ---------- | ----------- | ---------- |
| id         | bigint      | PK         |
| name       | varchar(50) | unique     |
| created_at | timestamp   |            |
| updated_at | timestamp   |            |

---

## 📌 `users`

| Column        | Type         | Constraint                  |
| ------------- | ------------ | --------------------------- |
| id            | bigint       | PK                          |
| name          | varchar(100) |                             |
| email         | varchar(100) | unique                      |
| password      | varchar(255) |                             |
| role_id       | bigint       | FK → roles.id               |
| employee_id   | bigint       | nullable, FK → employees.id |
| is_active     | boolean      | default true                |
| last_login_at | timestamp    | nullable                    |
| created_at    | timestamp    |                             |
| updated_at    | timestamp    |                             |

Index:

* role_id
* employee_id

---

# 🧱 2️⃣ Organization Structure

---

## 📌 `departments`

| Column     | Type         | Constraint                    |
| ---------- | ------------ | ----------------------------- |
| id         | bigint       | PK                            |
| name       | varchar(100) |                               |
| parent_id  | bigint       | nullable, FK → departments.id |
| created_at | timestamp    |                               |
| updated_at | timestamp    |                               |

Index:

* parent_id

---

## 📌 `positions`

| Column     | Type         | Constraint |
| ---------- | ------------ | ---------- |
| id         | bigint       | PK         |
| name       | varchar(100) |            |
| level      | integer      |            |
| created_at | timestamp    |            |
| updated_at | timestamp    |            |

---

# 🧱 3️⃣ Employees (Core Table)

---

## 📌 `employees`

| Column            | Type                                                | Constraint                  |
| ----------------- | --------------------------------------------------- | --------------------------- |
| id                | bigint                                              | PK                          |
| employee_code     | varchar(50)                                         | unique                      |
| full_name         | varchar(150)                                        |                             |
| nik               | varchar(50)                                         | unique                      |
| birth_date        | date                                                |                             |
| gender            | enum('male','female')                               |                             |
| phone             | varchar(20)                                         |                             |
| address           | text                                                |                             |
| hire_date         | date                                                |                             |
| employment_status | enum('probation','permanent','contract','resigned') |                             |
| department_id     | bigint                                              | FK → departments.id         |
| position_id       | bigint                                              | FK → positions.id           |
| manager_id        | bigint                                              | nullable, FK → employees.id |
| basic_salary      | decimal(15,2)                                       |                             |
| created_at        | timestamp                                           |                             |
| updated_at        | timestamp                                           |                             |

Index:

* department_id
* position_id
* manager_id

---

# 🧱 4️⃣ Attendance Module

---

## 📌 `attendances`

| Column         | Type                                    | Constraint        |
| -------------- | --------------------------------------- | ----------------- |
| id             | bigint                                  | PK                |
| employee_id    | bigint                                  | FK → employees.id |
| date           | date                                    |                   |
| check_in_time  | time                                    | nullable          |
| check_out_time | time                                    | nullable          |
| check_in_lat   | decimal(10,7)                           | nullable          |
| check_in_long  | decimal(10,7)                           | nullable          |
| check_out_lat  | decimal(10,7)                           | nullable          |
| check_out_long | decimal(10,7)                           | nullable          |
| status         | enum('present','late','absent','leave') |                   |
| created_at     | timestamp                               |                   |
| updated_at     | timestamp                               |                   |

Unique:

* (employee_id, date)

Index:

* employee_id
* date

---

# 🧱 5️⃣ Leave Management

---

## 📌 `leave_types`

| Column         | Type         | Constraint |
| -------------- | ------------ | ---------- |
| id             | bigint       | PK         |
| name           | varchar(100) |            |
| quota_per_year | integer      |            |
| created_at     | timestamp    |            |
| updated_at     | timestamp    |            |

---

## 📌 `leaves`

| Column        | Type                                  | Constraint                  |
| ------------- | ------------------------------------- | --------------------------- |
| id            | bigint                                | PK                          |
| employee_id   | bigint                                | FK → employees.id           |
| leave_type_id | bigint                                | FK → leave_types.id         |
| start_date    | date                                  |                             |
| end_date      | date                                  |                             |
| total_days    | integer                               |                             |
| reason        | text                                  |                             |
| status        | enum('pending','approved','rejected') |                             |
| approved_by   | bigint                                | nullable, FK → employees.id |
| approved_at   | timestamp                             | nullable                    |
| created_at    | timestamp                             |                             |
| updated_at    | timestamp                             |                             |

Index:

* employee_id
* leave_type_id
* status

---

# 🧱 6️⃣ Payroll Module

---

## 📌 `payroll_periods`

| Column     | Type      | Constraint    |
| ---------- | --------- | ------------- |
| id         | bigint    | PK            |
| month      | integer   |               |
| year       | integer   |               |
| is_locked  | boolean   | default false |
| created_at | timestamp |               |
| updated_at | timestamp |               |

Unique:

* (month, year)

---

## 📌 `payrolls`

| Column            | Type          | Constraint              |
| ----------------- | ------------- | ----------------------- |
| id                | bigint        | PK                      |
| employee_id       | bigint        | FK → employees.id       |
| payroll_period_id | bigint        | FK → payroll_periods.id |
| basic_salary      | decimal(15,2) |                         |
| total_allowance   | decimal(15,2) | default 0               |
| total_deduction   | decimal(15,2) | default 0               |
| tax               | decimal(15,2) | default 0               |
| net_salary        | decimal(15,2) |                         |
| created_at        | timestamp     |                         |
| updated_at        | timestamp     |                         |

Unique:

* (employee_id, payroll_period_id)

Index:

* payroll_period_id

---

## 📌 `payroll_items`

| Column     | Type                          | Constraint       |
| ---------- | ----------------------------- | ---------------- |
| id         | bigint                        | PK               |
| payroll_id | bigint                        | FK → payrolls.id |
| type       | enum('allowance','deduction') |                  |
| name       | varchar(100)                  |                  |
| amount     | decimal(15,2)                 |                  |
| created_at | timestamp                     |                  |
| updated_at | timestamp                     |                  |

Index:

* payroll_id

---

# 🧱 7️⃣ Performance Review

---

## 📌 `performance_reviews`

| Column      | Type        | Constraint        |
| ----------- | ----------- | ----------------- |
| id          | bigint      | PK                |
| employee_id | bigint      | FK → employees.id |
| reviewer_id | bigint      | FK → employees.id |
| period      | varchar(20) |                   |
| score       | integer     |                   |
| notes       | text        |                   |
| created_at  | timestamp   |                   |
| updated_at  | timestamp   |                   |

Index:

* employee_id
* reviewer_id

---

# 🧱 8️⃣ Audit Log (Enterprise Level)

---

## 📌 `audit_logs`

| Column     | Type         | Constraint    |
| ---------- | ------------ | ------------- |
| id         | bigint       | PK            |
| user_id    | bigint       | FK → users.id |
| action     | varchar(50)  |               |
| table_name | varchar(100) |               |
| record_id  | bigint       |               |
| old_values | json         | nullable      |
| new_values | json         | nullable      |
| created_at | timestamp    |               |

Index:

* user_id
* table_name
* record_id

---

# Total Tables Saat Ini

1. roles
2. users
3. departments
4. positions
5. employees
6. attendances
7. leave_types
8. leaves
9. payroll_periods
10. payrolls
11. payroll_items
12. performance_reviews
13. audit_logs

Total: **13 tables**

---