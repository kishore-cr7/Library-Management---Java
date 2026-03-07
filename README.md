<div align="center">

# 📚 Library Management System — Java

A **desktop-based Library Management System** built with **Java Swing** and **Oracle Database (JDBC)**, developed using the **NetBeans IDE**. This application streamlines core library operations including book cataloguing, student registration, book issuing/returning, searching, and review collection — all through a rich graphical user interface.

![Java](https://img.shields.io/badge/Language-Java-orange?logo=java)
![Swing](https://img.shields.io/badge/GUI-Java%20Swing-blue)
![Oracle](https://img.shields.io/badge/Database-Oracle%20XE-red?logo=oracle)
![IDE](https://img.shields.io/badge/IDE-NetBeans-green?logo=apache-netbeans-ide)

</div>

---

## 📖 Table of Contents

- [About the Project](#-about-the-project)
- [Features](#-features)
- [Tech Stack](#-tech-stack)
- [Project Structure](#-project-structure)
- [Database Schema](#-database-schema)
- [Prerequisites](#-prerequisites)
- [How to Run](#-how-to-run)
- [Application Workflow](#-application-workflow)
- [Screenshots](#-screenshots)
- [Future Enhancements](#-future-enhancements)

---

## 🔍 About the Project

This is a **college/educational mini-project** that demonstrates a complete Library Management workflow using **Object-Oriented Programming** in Java. The system provides two roles:

| Role | Capabilities |
|------|-------------|
| **Admin** | Add/edit/delete books, manage students, view issue & return records, access the admin dashboard |
| **Student** | Browse the book catalogue, get issued books, return books with ratings, search books, write reviews |

The entire UI is built with **Java Swing** using the **NetBeans GUI Builder** (`.form` + `.java` pairs), and all data is persisted in an **Oracle XE** database via **JDBC** (PreparedStatements).

---

## ✨ Features

| Module | Description |
|--------|-------------|
| 🔐 **Login & Signup** | Role-based authentication (Admin / Student). New students can self-register. |
| 🏠 **Dashboard** | Home screen displays live summary — total books, issued books, registered students, available books. |
| 📕 **Add Books** | Admin can add new books with ISBN, title, author, genre, page count, and quantity. |
| 📋 **Manage Books** | View, edit, and delete books from the catalogue. |
| 📤 **Issue Book** | Issue a book to a logged-in student with a selected return date. Automatically decrements the book quantity. |
| 📥 **Return Book** | Student returns a book and provides a star rating (1–5). Quantity is incremented back. |
| 🔍 **Search** | Search books by ISBN or Book Name. Displays average rating and review summary. |
| 👨‍🎓 **Student Management** | Admin can view and search registered students. |
| 📝 **Records** | View all issue and return records, filterable by Student ID or ISBN. |
| ⭐ **Reviews** | Students can leave written reviews after returning a book. |
| ⚠️ **Alerts** | Login reminder to return overdue books. Validation alerts for incomplete form fields. |

---

## 🛠 Tech Stack

| Layer | Technology |
|-------|-----------|
| **Language** | Java 8+ |
| **GUI Framework** | Java Swing (NetBeans GUI Builder) |
| **Database** | Oracle Database XE (Express Edition) |
| **Connectivity** | JDBC (`oracle.jdbc.driver.OracleDriver`) |
| **Date Picker** | JCalendar — `JDateChooser` (Toedter library) |
| **IDE** | Apache NetBeans |
| **Design Tool** | Oracle SQL Data Modeler (ER Diagram) |

---

## 📁 Project Structure

```
Library-Management---Java/
│
├── main/                            # NetBeans project root
│   ├── build.xml                    # Ant build script
│   ├── manifest.mf                  # JAR manifest
│   ├── nbproject/                   # NetBeans project metadata
│   ├── build/                       # Compiled output
│   └── src/
│       └── min/                     # Source package (all Java + Form files)
│           ├── Min.java             # Main entry point class
│           ├── loginn.java/.form    # Login screen (Admin / Student)
│           ├── signup.java/.form    # Student registration
│           ├── home.java/.form      # Admin dashboard
│           ├── shome.java/.form     # Student dashboard
│           ├── addbooks.java/.form  # Add new books
│           ├── managebooks.java/.form # View/edit/delete books
│           ├── issue.java/.form     # Issue book to student
│           ├── returnbook.java/.form # Return book with rating
│           ├── search.java/.form    # Search books (by name/ISBN)
│           ├── student.java/.form   # View/search students
│           ├── records.java/.form   # View issue & return records
│           └── review.java/.form    # Submit a book review
│
├── ER diagram/                      # Oracle SQL Data Modeler files
├── erdiagram.png                    # ER diagram image
├── schema.png                       # Database schema image
├── Library management rep-java.pdf  # Project report document
├── er.dmd                           # Data Modeler design file
└── README.md
```

---

## 🗃 Database Schema

The application expects an **Oracle XE** database with the following tables:

### Tables

```sql
-- 1. Books Table
CREATE TABLE books (
    isbn      NUMBER PRIMARY KEY,
    bookname  VARCHAR2(100),
    genre     VARCHAR2(50),
    author    VARCHAR2(100),
    page      NUMBER,
    quantity  NUMBER,
    rating    NUMBER DEFAULT 0
);

-- 2. Students Table
CREATE TABLE newstudent (
    studentid   NUMBER PRIMARY KEY,
    studentname VARCHAR2(100),
    password    VARCHAR2(50),
    contact     NUMBER,
    email       VARCHAR2(100)
);

-- 3. Admin Table
CREATE TABLE admin (
    name VARCHAR2(50),
    pass VARCHAR2(50)
);

-- 4. Issue Table
CREATE TABLE issue (
    isbn        NUMBER,
    bookname    VARCHAR2(100),
    studentid   NUMBER,
    studentname VARCHAR2(100),
    issuedate   DATE,
    duedate     DATE
);

-- 5. Return Book Table
CREATE TABLE returnbook (
    isbn        NUMBER,
    bookname    VARCHAR2(100),
    studentid   NUMBER,
    studentname VARCHAR2(100),
    issuedate   DATE,
    returndate  DATE,
    ratings     NUMBER
);

-- 6. Review Table
CREATE TABLE review (
    studentname VARCHAR2(100),
    bookname    VARCHAR2(100),
    isbn        NUMBER,
    review      VARCHAR2(500),
    studentid   NUMBER
);
```

### ER Diagram

The ER diagram and schema images in this repository illustrate the relationships between these entities.

---

## ⚙ Prerequisites

Before running the application, ensure you have the following installed:

| Requirement | Details |
|------------|---------|
| **JDK** | Java 8 or higher ([Download](https://www.oracle.com/java/technologies/downloads/)) |
| **Oracle Database XE** | Oracle Express Edition 11g/18c/21c ([Download](https://www.oracle.com/database/technologies/xe-downloads.html)) |
| **NetBeans IDE** | Apache NetBeans 12+ recommended ([Download](https://netbeans.apache.org/)) |
| **Oracle JDBC Driver** | `ojdbc8.jar` or `ojdbc11.jar` (included with Oracle or [download separately](https://www.oracle.com/database/technologies/appdev/jdbc-downloads.html)) |
| **JCalendar Library** | `jcalendar-1.4.jar` by Toedter ([Download](https://toedter.com/jcalendar/)) |

---

## 🚀 How to Run

### Step 1 — Set Up the Database

1. Install and start **Oracle Database XE**.
2. Open **SQL*Plus** or **SQL Developer** and connect as `system` (or create a dedicated user).
3. Run the SQL `CREATE TABLE` statements listed in the [Database Schema](#-database-schema) section above.
4. Insert at least one admin record:
   ```sql
   INSERT INTO admin VALUES ('admin', 'admin123');
   COMMIT;
   ```

### Step 2 — Configure the JDBC Connection

The project uses a hard-coded connection string across all Java files:

```java
DriverManager.getConnection("jdbc:oracle:thin:@localhost:1521:xe", "system", "<your-password>");
```

> ⚠️ **Important:** Open each `.java` file under `main/src/min/` and update the password (`15-06-2005`) to match your Oracle database password.

### Step 3 — Open in NetBeans

1. Launch **NetBeans IDE**.
2. Go to `File` → `Open Project` → navigate to the `main/` folder and open it.
3. **Add Libraries** to the project:
   - Right-click the project → `Properties` → `Libraries` → `Add JAR/Folder`.
   - Add `ojdbc8.jar` (Oracle JDBC driver).
   - Add `jcalendar-1.4.jar` (JCalendar date picker).

### Step 4 — Build & Run

1. Right-click the project → **Clean and Build**.
2. Run the `loginn.java` file (right-click → `Run File`), which launches the **Login Screen**.
3. Log in as **Admin** or **Student** to access the respective dashboards.

### Alternative — Run from Command Line

```bash
# Navigate to the build output directory
cd main/build/classes

# Run with required JARs on the classpath
java -cp ".;path/to/ojdbc8.jar;path/to/jcalendar-1.4.jar" min.loginn
```

---

## 🔄 Application Workflow

```
                        ┌──────────────┐
                        │  Login Screen │
                        └──────┬───────┘
                               │
                 ┌─────────────┴─────────────┐
                 │                           │
          ┌──────▼──────┐            ┌───────▼───────┐
          │ Admin Login  │            │ Student Login  │
          └──────┬──────┘            └───────┬───────┘
                 │                           │
          ┌──────▼──────┐            ┌───────▼───────┐
          │  Admin Home  │            │ Student Home   │
          │  (Dashboard) │            │  (Dashboard)   │
          └──────┬──────┘            └───────┬───────┘
                 │                           │
    ┌────────────┼────────────┐     ┌────────┼────────┐
    │            │            │     │        │        │
┌───▼───┐  ┌────▼────┐  ┌───▼──┐ ┌▼────┐ ┌─▼──┐ ┌──▼───┐
│Add    │  │Manage   │  │View  │ │Issue│ │Ret-│ │Search│
│Books  │  │Books    │  │Stud- │ │Book │ │urn │ │Books │
│       │  │         │  │ents  │ │     │ │Book│ │      │
└───────┘  └─────────┘  └──────┘ └──┬──┘ └──┬─┘ └──────┘
                                     │       │
                                     │  ┌────▼────┐
                                     │  │ Review & │
                                     │  │ Rating   │
                                     │  └─────────┘
                                     │
                                ┌────▼─────┐
                                │ Records  │
                                └──────────┘
```

**Key Processes:**

1. **Login** → User selects role (Admin/Student) and enters credentials validated against the database.
2. **Signup** → New students register; data is inserted into `newstudent` table.
3. **Add Books** → Admin fills in book details → `INSERT INTO books`.
4. **Issue Book** → Student selects a book → `INSERT INTO issue` + `UPDATE books SET quantity = quantity - 1`.
5. **Return Book** → Student enters ISBN and rating → `INSERT INTO returnbook` + `DELETE FROM issue` + `UPDATE books SET quantity = quantity + 1`.
6. **Search** → Query `books` table by ISBN or name; shows average rating from `returnbook`.
7. **Review** → Student submits a text review → `INSERT INTO review`.

---

## 📸 Screenshots

<img width="877" height="575" alt="login" src="https://github.com/user-attachments/assets/baf33bf7-1dfd-4335-8ff0-a38bfe293152" />

<img width="530" height="621" alt="signup" src="https://github.com/user-attachments/assets/575368a9-79fe-4c91-bfeb-af84c03e9125" />

<img width="1096" height="681" alt="adminhome" src="https://github.com/user-attachments/assets/c185cd1d-002a-4a84-94fa-5b04a16c7185" />

<img width="901" height="728" alt="adddingbook" src="https://github.com/user-attachments/assets/f5cc1f1c-7d41-47ec-b98e-7718e44e18b0" />

<img width="1053" height="728" alt="savingbook" src="https://github.com/user-attachments/assets/5fdc104a-fa29-4cb8-b623-3f96ee7cbb9b" />

<img width="1175" height="747" alt="managing book" src="https://github.com/user-attachments/assets/ed61b4af-c0f5-4b89-a1a8-8c1147bb5d89" />

<img width="1131" height="714" alt="managingbook2" src="https://github.com/user-attachments/assets/3259e637-5687-45f5-9ee1-0c01ab8534f8" />

<img width="1051" height="678" alt="search" src="https://github.com/user-attachments/assets/6978f6e9-cd2e-41b1-b02f-3fd6f09e653a" />

<img width="1104" height="678" alt="issuebook" src="https://github.com/user-attachments/assets/e639e199-16cd-4c11-b2c7-e501b9f6ee3d" />

<img width="1047" height="713" alt="issuebook1" src="https://github.com/user-attachments/assets/702a181c-67de-4eaa-af43-dfccdfcfbd97" />

<img width="1064" height="745" alt="issue succes" src="https://github.com/user-attachments/assets/4be546ed-5ed4-4f14-b081-49e3372179b9" />

<img width="1067" height="667" alt="returnbook" src="https://github.com/user-attachments/assets/d06c2c0b-8248-4d14-83cd-5fb02762a2e0" />

<img width="1072" height="669" alt="returnsucces" src="https://github.com/user-attachments/assets/449b9903-0816-4d3e-b8b7-3e3102cf6faa" />

<img width="1139" height="649" alt="alert" src="https://github.com/user-attachments/assets/35fbd250-e1b1-4dd2-af66-20631c9245c5" />

---



---

<div align="center">

**Made with ❤️ in Java**

</div>
