# Smart School Management System

> **A comprehensive web-based platform designed to streamline school administration by digitizing academic and operational workflows.**

## 1. The Elevator Pitch
The Smart School Management System centralizes student enrollment, attendance tracking, and performance analysis into a single, role-based dashboard. It empowers schools to manage data efficiently and transparently, providing dedicated portals for Admins, Teachers, and Students.

---

## 2. Technical Stack
* **Languages:** JavaScript (ES6+)
* **Frontend:** React.js, Redux (Toolkit), Material UI (MUI), Styled Components
* **Backend:** Node.js, Express.js
* **Database:** MongoDB, Mongoose
* **Tools/DevOps:** Netlify, Git, VS Code

---

## 3. Key Features
* **Multi-Role Access Control:** Secure portals for Admins, Teachers, and Students with specific permissions.
* **Academic Performance Tracking:** Stores and visualizes exam results using embedded document structures for fast retrieval.
* **Digital Attendance System:** Real-time attendance marking and "Clear All" functionality for efficient record-keeping.
* **Communication Hub:** Integrated systems for Notices and Complaints (student-to-admin feedback loop).

---

## 4. Engineering Highlights
* **Multi-Tenant Data Architecture:** All entities are strictly scoped to a specific `school` ID, allowing the system to host multiple independent schools securely.
* **Embedded Analytics Data:** Student documents embed `examResult` and `attendance` arrays, optimizing read performance for individual student dashboards by eliminating costly joins.

---

## 5. System Architecture
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

---

## 6. Database Schema
| Collection | Description | Key Fields |
| :--- | :--- | :--- |
| **Admin** | Manages the school instance. | `name`, `email`, `password`, `schoolName` |
| **Student** | Enrolled student data. | `name`, `rollNum`, `sclassName` (Ref), `attendance` |
| **Teacher** | Faculty members. | `name`, `email`, `teachSubject` (Ref), `teachSclass` (Ref) |
| **Sclass** | Standardized class/grade. | `sclassName`, `school` (Ref) |
| **Subject** | Academic subjects. | `subName`, `subCode`, `sessions`, `teacher` (Ref) |

---

## 7. API Routes Overview
| Resource | Key Endpoints | Description |
| :--- | :--- | :--- |
| **Admin** | `/AdminReg`, `/AdminLogin` | Registration & Login |
| **Student** | `/StudentReg`, `/StudentAttendance/:id` | Management & Attendance |
| **Teacher** | `/TeacherReg`, `/TeacherSubject` | Faculty Management |
| **Sclass** | `/SclassCreate`, `/SclassList/:id` | Class Structure |

---

## 🚀 Getting Started

### Prerequisites
- Node.js
- MongoDB
- npm / yarn

### Installation

1. Clone the repository:
```bash
git clone https://github.com/KmSasikumar/Mern-School-Management.git
```

2. Navigate to the project directory:
```bash
cd Mern-School-Management
```

3. Install dependencies for both frontend and backend:
```bash
# For frontend
cd frontend
npm install

# For backend
cd ../backend
npm install
```

4. Set up environment variables (`.env`) for backend (Mongo URI, JWT secret, etc.)

5. Start the development servers:
```bash
# Start backend
npm run server

# Start frontend
npm start
```

## 📸 Screenshots

### 🖼️ Main Page  
![Main Page](Photos/Main%20page.png)

### 🖼️ Selection Page  
![Selection Page](Photos/Selection%20Page.png)

---

## 👨‍💻 Author
**K. Sasi Kumar**
* 🎓 VIT Bhopal University
* 📧 Kommamani012@gmail.com
* 📱 +91 8985037606
