# STUDENT ATTENDANCE MANAGEMENT SYSTEM (SAMS)

**Course:** INFO 3305 Web Application Development  
**Semester:** 1, 2025/2026 — Section 4  
**Submission deadline:** 12/12/2025

---

## Group Members
- Ahmad Faiz bin Abdul Karim — **2316083**  
- Puteri Areefa Aura binti Kamaruzzaman — **2319958**  
- Zarith Sofea binti Hazzarul Hisham — **2315270**  
- Nor Syazana binti Mohd Ansar — **2319258**  
- Nur Maisarah binti Roslan — **2311284**

---

## Project Title
**Student Attendance Management System (SAMS)**

---

## 1. Introduction
SAMS is a web-based Model-View-Controller (MVC) application developed using the **Laravel** framework and a **MySQL** database. The system digitizes attendance recording and management for educational institutions, replacing manual registers with a centralized, secure, and responsive dashboard. This enables lecturers and administrators to efficiently record attendance, generate reports, and monitor attendance trends for academic analysis.

---

## 2. Objectives
- Automate attendance recording to reduce manual errors and time consumption.  
- Maintain a centralized relational database for students, classes, and attendance records.  
- Provide role-based access: admin and lecturer.  
- Enable easy generation of attendance reports and export options (CSV/PDF).  
- Offer a responsive, user-friendly dashboard accessible from multiple devices.  
- Follow Laravel’s MVC pattern for clean separation of concerns and maintainability.

---

## 3. Features & Functionalities
### Core Features
- **User Authentication**: Secure login for Admin and Lecturers (Laravel Auth).  
- **Role Management**: Admin and Lecturer roles with different permissions.  
- **Student Management**: Add/edit/delete student records (name, matric no, class, contact).  
- **Class / Course Management**: Create and manage classes/sessions and assign lecturers.  
- **Attendance Recording**: Mark attendance per class session (Present / Absent / Excused).  
- **Attendance Editing**: Edit previously marked attendance with audit log.  
- **Report Generation**: Generate attendance reports by student, class, date range and export to CSV/PDF.  
- **Dashboard & Insights**: Charts and summary — total attendance, absent rates, and recent activity.  
- **Responsive UI**: Works on desktop and mobile using Blade + CSS (optionally Tailwind or Bootstrap).

---

## 4. System Architecture (MVC)
- **Model**: Eloquent models — User, Student, Class, Session, Attendance, Role, AuditLog.  
- **View**: Blade templates for login, dashboards, forms, and reports.  
- **Controller**: Handles HTTP requests, validation, and business rules; uses repositories or service classes where appropriate.

---

## 5. Database Design (ERD)

```mermaid
erDiagram
    Classrooms {
        int id PK
        string name
        int teacher_id
        datetime updated_at
        datetime created_at
    }

    Students {
        int id PK
        string name
        int student_id
        int classroom_id FK
        datetime created_at
    }

    Attendances {
        int id PK
        date date
        string status
        int student_id FK
        datetime created_at
    }

    Classrooms ||--o{ Students : "has"
    Students ||--o{ Attendances : "records"

---

## 6. Sequence Diagram

sequenceDiagram
    autonumber

    participant T as Teacher (User)
    participant V as Web Browser (View)
    participant C as Laravel Controller
    participant M as Model (Eloquent/DB)

    T ->> V: Open "Mark Attendance" Page
    V ->> C: GET /attendance/create
    C ->> M: Retrieve class and student list
    M -->> C: Return data
    C -->> V: Render attendance form (Blade View)
    V -->> T: Display Attendance Form

    T ->> V: Submit attendance data
    V ->> C: POST /attendance/store
    C ->> M: Save attendance record
    M -->> C: Confirm success
    C -->> V: Redirect to attendance list view
    V -->> T: Display "Attendance Recorded Successfully"
