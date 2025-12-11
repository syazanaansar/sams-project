# STUDENT ATTENDANCE MANAGEMENT SYSTEM (SAMS)

**Course:** INFO 3305 Web Application Development  
**Semester:** 1, 2025/2026 — Section 4  
**Submission deadline:** 11/12/2025

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

### Additional (Optional)
- Student self-service portal to view personal attendance.  
- Email notifications for low attendance.  
- Bulk upload of students via CSV.  
- API endpoints for integration.

---

## 4. System Architecture (MVC)
- **Model**: Eloquent models — User, Student, Class, Session, Attendance, Role, AuditLog.  
- **View**: Blade templates for login, dashboards, forms, and reports.  
- **Controller**: Handles HTTP requests, validation, and business rules; uses repositories or service classes where appropriate.

---

## 5. Database Design (ERD)
Below is the ERD in Mermaid `erDiagram` syntax (GitHub supports rendering Mermaid):

```mermaid
erDiagram
    USERS {
        int id PK
        string name
        string email
        string password
        string role
        timestamp created_at
        timestamp updated_at
    }

    STUDENTS {
        int id PK
        string name
        string matric_no
        string email
        int class_id FK
        timestamp created_at
        timestamp updated_at
    }

    CLASSES {
        int id PK
        string code
        string name
        int lecturer_id FK
        timestamp created_at
        timestamp updated_at
    }

    SESSIONS {
        int id PK
        int class_id FK
        date session_date
        time start_time
        time end_time
        string topic
        timestamp created_at
        timestamp updated_at
    }

    ATTENDANCES {
        int id PK
        int session_id FK
        int student_id FK
        enum status  /* Present/Absent/Excused */
        string remark
        timestamp created_at
        timestamp updated_at
    }

    AUDIT_LOGS {
        int id PK
        int user_id FK
        string action
        text details
        timestamp created_at
    }

    USERS ||--o{ CLASSES : "lectures"
    CLASSES ||--o{ SESSIONS : "has"
    SESSIONS ||--o{ ATTENDANCES : "records"
    STUDENTS ||--o{ ATTENDANCES : "attends"
    CLASSES ||--o{ STUDENTS : "contains"
    USERS ||--o{ AUDIT_LOGS : "creates"
    STUDENTS }|..|{ CLASSES : "assigned_to"

