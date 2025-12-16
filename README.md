# Library-Management---Java

This repository contains a college/educational desktop Library Management System implemented in Java. It is a NetBeans/Swing-based application that demonstrates core library operations: managing books and students, issuing and returning books, searching the catalogue, and collecting simple reviews. The code is written with a focus on demonstrating object‑oriented design, JDBC persistence, and a small GUI built from NetBeans form templates.



Java source (NetBeans-style Swing forms) under main/src/min — GUI windows and controllers.
A project report PDF documenting design choices and requirements.
ER diagram and schema images that describe the database model and relationships.
Example screenshots and other design artifacts.
Core features

Book management: add, edit and remove books; each record stores ISBN, title, author, genre, page count and quantity.
Student/member management: register and list students with ID, name, password, contact and email.
Issue and return flows: record issuance of books to students and process returns; code looks up current loans for a student and updates counts.
Dashboard: home screens show summary counts (total books, issued books, students, available books).
Search and browse: populate and search the book list; results displayed in Swing tables.
Reviews: a simple feedback form is included to capture user reviews for a selected book.
Important implementation details

GUI: The user interface is implemented with Swing and NetBeans GUI builder templates (frame classes such as home, shome, addbooks, issue, returnbook, student, signup, search, review).
Entry point: a basic main class (Min) exists; the practical UI entry is managed by the GUI frames created from the NetBeans project.
Persistence: The app uses JDBC to talk to an Oracle database. SQL queries in the source reference tables named like books, newstudent and issue. Database calls are placed inside GUI classes and populate Swing table models directly from ResultSets.
External components: the project references a Swing date chooser (JDateChooser) and requires the Oracle JDBC driver on the classpath.
Hard-coded configuration: many classes use a hard-coded connection string and credentials that point to Oracle XE on localhost (the code shows usage of the Oracle JDBC driver and a local XE URL). These values are present in source files and should be replaced or externalized before sharing or deploying.
Database model (what the code expects)

The code assumes a relational schema with at least:
books (isbn, bookname, genre, author, page, quantity, rating)
newstudent (student id, name, password, contact, email)
issue (studentid, isbn, issue-related fields)
ER diagram and schema images in the repository document the relationships; use those diagrams to create matching SQL tables in your database.
Dependencies and environment notes

Java 8+ (or a compatible JDK) to compile and run the Swing app.
Oracle JDBC driver (ojdbc) must be present on the runtime classpath for database connectivity.
JCalendar (toedter) library is referenced for date chooser UI components.
The project was developed with NetBeans; opening the project in NetBeans preserves form metadata and simplifies editing UI forms.
The code currently connects using the system Oracle account in source examples — create a restricted application user and move credentials out of source code for security.
How the application is intended to be used (conceptual)

Prepare the database according to the schema shown in the ER diagram and ensure the application user has the necessary privileges.
Place required JDBC and UI library JARs on the application classpath.
Launch the GUI (NetBeans can run the project directly; otherwise run the compiled application through your Java runtime).
Use the GUI to register students, add books, issue and return books, and view dashboard statistics. The UI tables and forms reflect database rows and update via JDBC calls.
Practical caveats and recommendations

Externalize DB configuration: move host, port, user and password into a properties file or environment variables instead of hard-coding them in multiple classes.
Use a dedicated database user (not system) with minimal privileges for the application.
Separate business logic from GUI code: move core loan and validation logic into plain Java classes to ease testing and maintenance.
Add basic unit tests for loan rules, availability calculations and input validation.
If you include many or large images (screenshots), consider Git LFS to avoid repository bloat.
Suggested next improvements

Replace in‑class JDBC connection strings with a single configuration mechanism.
Add database creation scripts (SQL) derived from the ER diagram so new users can quickly set up an example database.
Move to a lightweight embedded database (H2/SQLite) for easier local testing, or provide a sample Oracle export.
Introduce role-based access (admin/staff/member) and basic authentication flows.
Add input validation, error handling and logging to make the app robust for practical use.

------------------------------------------------------------------------------------------------------------------------------------------------------------------------
Screen Shots

<img width="901" height="728" alt="adddingbook" src="https://github.com/user-attachments/assets/f5cc1f1c-7d41-47ec-b98e-7718e44e18b0" />
<img width="1096" height="681" alt="adminhome" src="https://github.com/user-attachments/assets/c185cd1d-002a-4a84-94fa-5b04a16c7185" />
<img width="530" height="621" alt="signup" src="https://github.com/user-attachments/assets/575368a9-79fe-4c91-bfeb-af84c03e9125" />
<img width="1051" height="678" alt="search" src="https://github.com/user-attachments/assets/6978f6e9-cd2e-41b1-b02f-3fd6f09e653a" />
<img width="1053" height="728" alt="savingbook" src="https://github.com/user-attachments/assets/5fdc104a-fa29-4cb8-b623-3f96ee7cbb9b" />
<img width="1072" height="669" alt="returnsucces" src="https://github.com/user-attachments/assets/449b9903-0816-4d3e-b8b7-3e3102cf6faa" />
<img width="1067" height="667" alt="returnbook" src="https://github.com/user-attachments/assets/d06c2c0b-8248-4d14-83cd-5fb02762a2e0" />
<img width="1131" height="714" alt="managingbook2" src="https://github.com/user-attachments/assets/3259e637-5687-45f5-9ee1-0c01ab8534f8" />
<img width="1175" height="747" alt="managing book" src="https://github.com/user-attachments/assets/ed61b4af-c0f5-4b89-a1a8-8c1147bb5d89" />
<img width="877" height="575" alt="login" src="https://github.com/user-attachments/assets/baf33bf7-1dfd-4335-8ff0-a38bfe293152" />
<img width="1047" height="713" alt="issuebook1" src="https://github.com/user-attachments/assets/702a181c-67de-4eaa-af43-dfccdfcfbd97" />
<img width="1104" height="678" alt="issuebook" src="https://github.com/user-attachments/assets/e639e199-16cd-4c11-b2c7-e501b9f6ee3d" />
<img width="1064" height="745" alt="issue succes" src="https://github.com/user-attachments/assets/4be546ed-5ed4-4f14-b081-49e3372179b9" />
<img width="1139" height="649" alt="alert" src="https://github.com/user-attachments/assets/35fbd250-e1b1-4dd2-af66-20631c9245c5" />
