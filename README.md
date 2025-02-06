# Column-Level-Security-CLS-in-PostgreSQL
Column-Level Security (CLS) is about controlling which columns users can access in a table. 🛡️ Instead of giving access to all columns, we allow access to just specific ones. This helps us keep sensitive data secure! 🔒

## Ways to Implement CLS in PostgreSQL 💡

### 1. Using Views 👀
Views allow us to create a virtual table that only shows certain columns from the original table. 🚀

- Create the table 📋
```sql
CREATE TABLE employees (
    employee_id SERIAL PRIMARY KEY,
    name VARCHAR(100),
    email VARCHAR(100),
    salary DECIMAL(10, 2),
    department VARCHAR(100)
);
```

- Create a View with limited columns 👓:
```sql
CREATE VIEW public_employee_view AS
SELECT employee_id, name, department
FROM employees;
```

- Grant access to the view 🌐:
```sql
GRANT SELECT ON public_employee_view TO user_name;
```

- Revoke access from the table ❌:
```sql
REVOKE SELECT ON employees FROM user_name;
```

### 2. Using Roles 🎭

- Create roles 🎟️:
```sql
CREATE ROLE role_with_access;
CREATE ROLE role_without_access;
```

- Assign columns to roles ✨:
```sql
GRANT SELECT (employee_id, name, salary) ON employees TO role_with_access;
GRANT SELECT (employee_id, name, department) ON employees TO role_without_access;
```

- Grant the roles to users 👥:
```sql
GRANT role_with_access TO user_name_with_access;
GRANT role_without_access TO user_name_without_access;
```

