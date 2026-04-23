# 🔬 Research Project Management System (RPMS)

A fully normalized relational database system designed to manage all research projects of an academic institute — tracking faculty, students, sponsors, budgets, progress reports, and publications in one unified platform.

> Built as a DBMS course project at **DA-IICT** by Group 56.

---

## 📌 Table of Contents

- [About the Project](#about-the-project)
- [Features](#features)
- [Tech Stack](#tech-stack)
- [Database Design](#database-design)
- [ER Diagram](#er-diagram)
- [Schema Overview](#schema-overview)
- [Normalization](#normalization)
- [SQL Queries](#sql-queries)
- [Setup & Usage](#setup--usage)
- [JDBC Connectivity](#jdbc-connectivity)
- [Front-End Screenshots](#front-end-screenshots)
- [Known Limitations](#known-limitations)
- [Authors](#authors)

---

## 📖 About the Project

The **Research Project Management System (RPMS)** is a database-driven application that provides a centralized platform for institutes to manage their research activities. It handles:

- Project tracking with deadlines and status
- Faculty supervision and student assignments
- Sponsor and funding management
- Progress report submissions
- Publication records
- Role-based user access (Admin, Faculty, Student, Sponsor)

The database design follows the complete lifecycle: requirements gathering → ER modeling → relational model → normalization (up to 3NF/BCNF) → DDL scripts → data population → SQL queries → Java/JDBC front-end.

---

## ✨ Features

- **Project Management** — Store and track research project details, objectives, timelines, and status
- **Role-Based Access** — Separate access levels for Administrators, Faculty, Students, and Sponsors
- **Budget Tracking** — Monitor total allocated vs. spent budget per project
- **Progress Reports** — Students can submit reports linked to their project and faculty
- **Publication Records** — Track research papers and journal publications per project
- **Sponsor Management** — Maintain sponsor details and their funding contributions
- **40+ SQL Queries** — Covering SELECT, JOINs, GROUP BY, subqueries, aggregate functions, and views

---

## 🛠 Tech Stack

| Layer | Technology |
|---|---|
| Database | MySQL |
| Backend Connectivity | Java (JDBC) |
| Query Language | SQL (DDL + DML) |
| Documentation | SRS (IEEE format) |

---

## 🗄 Database Design

### ER Diagram

> 📌 **[Add ER Diagram image here]**
> Export your finalized ER diagram as a PNG and place it in `/docs/er_diagram.png`, then uncomment the line below:

<!-- ![ER Diagram](docs/er_diagram.png) -->

Three iterations of the ER diagram were created during the design process:
1. **Initial ER Diagram** — First draft based on noun analysis
2. **Improved ER Diagram** — Refined after identifying missing relationships
3. **Finalized ER Diagram** — Clean, complete diagram used for the relational model

---

### Schema Overview

The database consists of the following tables:

| Table | Description |
|---|---|
| `Project` | Core table storing research project details |
| `Faculty` | Faculty members who supervise projects |
| `Student` | Students assigned to projects under faculty |
| `Administrator` | Institute admins managing the system |
| `Sponsor` | External sponsors funding projects |
| `ProgressReport` | Reports submitted by students for each project |
| `Publication` | Research papers and journal articles linked to projects |
| `Budget` | Budget allocation and spending per project |
| `Login_UserAccess` | User credentials and role-based access control |

---

## 📐 Normalization

The database was progressively normalized through the following stages:

### 1NF
- All attributes are atomic
- No repeating groups

### 2NF
- All non-key attributes are fully functionally dependent on the primary key
- Partial dependencies removed

### 3NF / BCNF
- Transitive dependencies eliminated
- All determinants are candidate keys
- Final schema is in **BCNF**

Detailed dependency analysis and anomaly analysis (insertion, update, deletion) are documented in the [SRS document](docs/Group56_FinalSRS.pdf).

---

## 💾 SQL Queries

The [`sql/queries.sql`](sql/queries.sql) file contains **40 SQL queries** including:

| Category | Examples |
|---|---|
| Basic SELECT | Fetch all projects, faculty, students |
| JOINs | Projects with faculty names, students with their projects |
| Aggregations | COUNT, SUM, AVG per faculty/sponsor |
| Subqueries | Students under CS faculty, projects over budget threshold |
| Views | `FacultyProjectView` for quick lookups |
| Filters | Overdue projects, Gmail users, low remaining budget |

---

## ⚙️ Setup & Usage

### Prerequisites
- MySQL 8.0+ installed
- Java JDK 8+ (for JDBC)
- MySQL Connector/J JAR

### Steps

**1. Clone the repository**
```bash
git clone https://github.com/YOUR_USERNAME/research-project-db.git
cd research-project-db
```

**2. Create the database**
```sql
CREATE DATABASE rpms_db;
USE rpms_db;
```

**3. Run the DDL script to create tables**
```bash
mysql -u root -p rpms_db < sql/ddl_schema.sql
```

**4. Populate the database with sample data**
```bash
mysql -u root -p rpms_db < sql/dml_insert.sql
```

**5. Run the queries**
```bash
mysql -u root -p rpms_db < sql/queries.sql
```

---

## 🔌 JDBC Connectivity

The [`jdbc/DBConnection.java`](jdbc/DBConnection.java) file demonstrates how to connect to the MySQL database using Java JDBC.

> 📌 **[Add JDBC code screenshot here]**
> Place screenshot at `/docs/screenshots/jdbc_connection.png`

<!-- ![JDBC Connection](docs/screenshots/jdbc_connection.png) -->

Update the connection string in the file with your credentials:
```java
String url = "jdbc:mysql://localhost:3306/rpms_db";
String user = "your_username";
String password = "your_password";
```

---

## 🖥 Front-End Screenshots

> 📌 **[Add front-end screenshots here]**
> Place screenshots in `/docs/screenshots/` and list them below:

<!-- ![Home Page](docs/screenshots/home.png) -->
<!-- ![Project Dashboard](docs/screenshots/dashboard.png) -->
<!-- ![Login Page](docs/screenshots/login.png) -->

---

## ⚠️ Known Limitations

- **Passwords are stored in plain text** in `Login_UserAccess` — in a production system, passwords should be hashed using bcrypt or SHA-256.
- **Single faculty per student** — the current schema supports only one faculty supervisor per student. A junction table would be needed for co-supervision scenarios.
- The `RemainingAmount` column in `Budget` is a derived value (`TotalAmount - SpentAmount`) and could be computed dynamically instead of stored.

---

## 👨‍💻 Authors

**Group 56 — DA-IICT**

| Name | Enrollment No. |
|---|---|
| Dhrumil Doshi | 202512088 |
| Harsh Abhichandani | 202512027 |

---

## 📄 License

This project was created for academic purposes as part of the DBMS course at DA-IICT.
