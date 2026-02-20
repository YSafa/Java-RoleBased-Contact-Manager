# CMPE 343 – Project 2: Role-Based Contact Management System

A console-based Contact Management System built with Java and MySQL as part of the CMPE 343 course at Kadir Has University. The application features role-based access control, secure password hashing, animated ASCII art startup/shutdown sequences, and full Turkish character support.

## 👥 Team – Group 29
- Dıldar Baştuğ
- Doğukan Furat
- Sena Coşkun
- Yiğit Safa Yıldırım

---

## ✨ Features

### 🔐 Authentication & Role-Based Access
Users log in with a username and password (stored as SHA-256 hashes). Upon login, the system identifies the user's role and displays the appropriate menu. The four supported roles and their permissions are:

| Role | Permissions |
|---|---|
| **Tester** | List contacts, search & sort, change password |
| **Junior Developer** | All Tester permissions + update contacts |
| **Senior Developer** | All Junior Dev permissions + add & delete contacts |
| **Manager** | User management (add/update/delete users), contact statistics |

### 📋 Contact Operations
- **List all contacts** with paginated, formatted output
- **Search** by single field (first name, last name, phone number) or multiple fields combined (e.g. name + birth month, phone substring + email substring)
- **Sort** results in ascending or descending order by any field
- **Add, update, delete** contacts (role-dependent)
- **Undo** the last add, update, or delete action via an undo stack

### 👤 Manager-Only: User Management
- List all system users
- Add new users / delete existing users
- Update user information
- View contact statistics (youngest/oldest contact, average age, LinkedIn coverage, most common names, etc.)

### 🎨 UI & UX
- Colorful ANSI console output
- ASCII art opening and closing animations
- Logged-in user's full name displayed at the top of every menu
- Robust input validation with clear error messages and retry prompts (never crashes on bad input)

---

## 🏗️ Project Structure

```
GroupSource29/
├── Group29.java              # Entry point — login flow & role delegation
├── users/
│   ├── User.java             # Abstract base class (encapsulation, polymorphism)
│   ├── Tester.java           # Tester role
│   ├── JuniorDeveloper.java  # Extends Tester
│   ├── SeniorDeveloper.java  # Extends JuniorDeveloper
│   └── Manager.java          # Extends SeniorDeveloper
├── interfaces/
│   ├── Searchable.java       # Search interface
│   └── Sortable.java         # Sort interface
└── utils/
    ├── DBUtils.java          # MySQL JDBC connection management
    ├── ConsoleUtils.java     # ANSI colors, screen clear, headers
    ├── AnimUtils.java        # Opening/closing ASCII animations
    └── PasswordUtils.java    # SHA-256 password hashing & verification
```

**OOP Principles Applied:**
- **Inheritance** — `JuniorDeveloper → Tester`, `SeniorDeveloper → JuniorDeveloper`, `Manager → SeniorDeveloper`
- **Abstraction** — `User` is an abstract class with `displayMenu()` enforced on all subclasses
- **Polymorphism** — Role-specific menu behavior via method overriding
- **Encapsulation** — User fields are `protected`; access is managed through methods

---

## 🛠️ Tech Stack
- **Language:** Java (multi-class, multi-package)
- **Database:** MySQL 8+ via JDBC
- **Security:** SHA-256 password hashing
- **Documentation:** JavaDoc

---

## ▶️ How to Run

### Requirements
- Java JDK 11 or higher
- MySQL Server running locally
- MySQL Connector/J (JDBC driver) JAR

### 1. Database Setup
```sql
-- Create the database and import the provided schema
mysql -u myuser -p cmpe343_proj2 < Group29.sql
```
Default DB credentials (as per course spec):
- **Host:** `localhost:3306`
- **Database:** `cmpe343_proj2`
- **Username:** `myuser`
- **Password:** `1234`

### 2. Compile
From the `GroupSource29/` directory:
```bash
javac -cp ".;mysql-connector-j-x.x.x.jar" Group29.java users/*.java interfaces/*.java utils/*.java
```
*(Use `:` instead of `;` on Linux/macOS)*

### 3. Run
```bash
java -cp ".;mysql-connector-j-x.x.x.jar" Group29
```

### Default Test Accounts
| Username | Password | Role |
|---|---|---|
| `tt` | `tt` | Tester |
| `jd` | `jd` | Junior Developer |
| `sd` | `sd` | Senior Developer |
| `man` | `man` | Manager |
