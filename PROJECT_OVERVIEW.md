# Smart School Management System - Project Overview

## 1. The Elevator Pitch
A comprehensive web-based platform designed to streamline school administration by digitizing academic and operational workflows. It centralizes student enrollment, attendance tracking, and performance analysis into a single, role-based dashboard, empowering schools to manage data efficiently and transparently.

## 2. Technical Stack
* **Languages:** JavaScript (ES6+)
* **Frontend:** React.js, Redux (Toolkit), Material UI (MUI), Styled Components
* **Backend:** Node.js, Express.js
* **Database:** MongoDB, Mongoose
* **Tools/DevOps:** Netlify (Configured), Git, vs Code

## 3. System Architecture

The following diagram illustrates the high-level architecture and data flow of the application.

```mermaid
graph TD
    subgraph "Users"
        A[Admin]
        T[Teacher]
        S[Student]
    end

    subgraph "Frontend (React + MUI)"
        UI[User Interface]
        Redux[Redux Store]
        Axios[Axios HTTP Client]
    end

    subgraph "Backend (Node.js + Express)"
        API[REST API Controllers]
        Auth[Authentication (Bcrypt)]
        Routes[Express Router]
    end

    subgraph "Database (MongoDB)"
        DB[(MongoDB Cluster)]
    end

    A -->|Manage School| UI
    T -->|Manage Class/Attendance| UI
    S -->|View Performance| UI

    UI --> Redux
    Redux --> Axios
    Axios -->|JSON Request| Routes
    Routes --> API
    API -->|Read/Write| DB
    API -->|Auth Check| Auth
```

## 4. Database Schema

The application uses **MongoDB** with **Mongoose** for object modeling. Below is the schema design optimized for critical school data.

| Collection | Description | Key Fields |
| :--- | :--- | :--- |
| **Admin** | Manages the school instance. One admin per school. | `name`, `email`, `password`, `schoolName` |
| **Student** | Represents a student enrolled in a class. | `name`, `rollNum`, `password`, `sclassName` (Ref), `attendance` (Embedded), `examResult` (Embedded) |
| **Teacher** | Faculty members managing subjects and classes. | `name`, `email`, `password`, `teachSubject` (Ref), `teachSclass` (Ref), `attendance` |
| **Sclass** | A standardized class or grade level. | `sclassName`, `school` (Ref) |
| **Subject** | Academic subjects taught in a class. | `subName`, `subCode`, `sessions`, `sclassName` (Ref), `teacher` (Ref) |
| **Notice** | Announcements visible to school members. | `title`, `details`, `date` |
| **Complain** | Issues raised by students. | `user` (Ref), `complaint`, `date`, `school` (Ref) |

## 5. API Routes Overview

Key API endpoints handling data operations between the client and server.

| Resource | Methods | Key Endpoints | Description |
| :--- | :--- | :--- | :--- |
| **Admin** | `POST`, `GET` | `/AdminReg`, `/AdminLogin`, `/Admin/:id` | Admin registration, login, and profile retrieval. |
| **Student** | `POST`, `GET`, `PUT`, `DELETE` | `/StudentReg`, `/StudentLogin`, `/Student/:id`, `/StudentAttendance/:id` | Complete CRUD for students, including grading and attendance marking. |
| **Teacher** | `POST`, `GET`, `DELETE`, `PUT` | `/TeacherReg`, `/TeacherLogin`, `/Teacher/:id` | Teacher management and profile access. |
| **Sclass** | `POST`, `GET`, `DELETE` | `/SclassCreate`, `/SclassList/:id`, `/Sclass/:id` | Creation and listing of school classes. |
| **Subject** | `POST`, `GET`, `DELETE` | `/SubjectCreate`, `/AllSubjects/:id`, `/ClassSubjects/:id` | Subject management linked to classes and teachers. |
| **Notice** | `POST`, `GET`, `DELETE` | `/NoticeCreate`, `/NoticeList/:id` | Posting and retrieving school-wide notices. |

## 6. Key Features (Functional)
* **Multi-Role Access Control:** Secure portals for Admins, Teachers, and Students with specific permissions.
* **Academic Performance Tracking:** Stores and visualizes exam results using embedded document structures for fast retrieval.
* **Digital Attendance System:** Real-time attendance marking and "Clear All" functionality for efficient record-keeping.
* **Communication Hub:** Integrated systems for Notices and Complaints (student-to-admin feedback loop).

## 7. Engineering Highlights
* **Multi-Tenant Data Architecture:**  All entities are strictly scoped to a specific `school` ID, allowing the system to host multiple independent schools securely.
* **Embedded Analytics Data:** Student documents embed `examResult` and `attendance` arrays, optimizing read performance for individual student dashboards by eliminating costly joins (lookups).
