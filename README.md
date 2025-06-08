# Oracle HR & Payroll Management System (PL/SQL)

This project is a **mini HR and Payroll system** built using **Oracle Live SQL** and **PL/SQL**. It demonstrates how to manage employees, record attendance, handle leave requests, and process monthly payroll, simulating real-world ERP functionality — perfect for showcasing skills relevant to Oracle Applications Labs (OAL).

## 🔧 Features

- **Employee Management**: Add and store employee details like name, department, position, hire date, and base salary.
- **Attendance Tracking**: Record daily hours worked and absence status.
- **Leave Management**:
  - Employees can request leaves with reasons and date ranges.
  - Managers can approve or reject leave requests.
  - Rejected leave days result in payroll deductions.
- **Payroll Processing**:
  - Calculates gross salary.
  - Deducts salary based on unworked hours (less than 160 hrs/month).
  - Deducts salary for unapproved leave days.
  - Stores payroll history per employee per month.
- **Robust Error Handling** using PL/SQL exceptions.

## 📁 Database Tables

- `employees`: Stores basic employee information.
- `attendance`: Tracks daily hours worked and absence info.
- `leave_requests`: Stores leave requests with approval tracking.
- `payroll_history`: Stores processed payroll data per employee/month.

## 💻 PL/SQL Procedures

### `request_leave(p_employee_id, p_start_date, p_end_date, p_reason)`
Submits a leave request with validations (e.g., start date must not be after end date).

### `approve_leave(p_request_id, p_manager_id, p_action)`
Approves or rejects a leave request. Accepts `APPROVE` or `REJECT` as valid actions.

### `process_payroll(p_employee_id, p_month)`
Processes an employee’s salary for the given month:
- Calculates gross pay from `base_salary`
- Deducts pay for missing work hours (less than 160 hours)
- Deducts pay for days of rejected leave requests
- Inserts payroll summary into `payroll_history`

##⚙️ Technologies Used

- Oracle Live SQL

- PL/SQL: Stored procedures, conditionals, error handling

- SQL: Table creation, constraints, inserts, selects

## 🧪 Sample Execution

```sql
-- Submit leave request
EXECUTE request_leave(4, DATE '2025-06-05', DATE '2025-06-06', 'Medical');

-- Approve leave request
EXECUTE approve_leave(2, 99, 'APPROVE');

-- Process payroll for employee ID 4 for June 2025
EXECUTE process_payroll(4, '2025-06');

-- View payroll history
SELECT * FROM payroll_history;

