# 🏨 Hostel Complaint Management System 🚀

A full-stack web application for managing hostel complaints with role-based access, built using React / Next.js, Tailwind CSS, and Supabase.

Built with Next.js and Supabase, this system enables students to submit and track hostel complaints in real time.

---

## 📌 Overview

The Hostel Complaint Management System streamlines complaint reporting and resolution inside hostels.

It provides:

- Role-based dashboards  
- Real-time complaint tracking  
- Structured workflow (Pending → Ongoing → Resolved)  
- Secure authentication  

---

## 🚀 Features

## 👤 Roles

### 🎓 Student
- Register & Login  
- Submit hostel complaints  
- Track complaint status  
- View complaint history  

### 🛠 Admin / Warden
- View all complaints  
- Change complaint status  
  - Pending → Ongoing → Resolved  
- Assign workers to complaints  
- Monitor resolution progress  

### 👷 Worker (Technician / Cleaner)
- Login using email  
- View assigned complaints  
- Update complaint progress  
- Mark complaints as resolved  

---

## 🏗️ Tech Stack

## 💻 Frontend
- React  
- Next.js (App Router)  
- Tailwind CSS  
- TypeScript  

## 🌐 Backend
- Next.js API Routes  
- Server Actions  

## 🗄️ Database & Authentication
- Supabase Auth  
- Supabase 

---

## 🔄 System Flow

```
Student submits complaint
        ⬇
Stored in Supabase Database
        ⬇
Admin assigns worker
        ⬇
Worker updates progress
        ⬇
Complaint marked as Resolved
```

---

## 🎯 Project Goal

Build a scalable complaint management system that can:

✔ Simplify hostel issue reporting  
✔ Improve resolution efficiency  
✔ Provide role-based dashboards  
✔ Track maintenance lifecycle clearly  

---

## 🚀 Future Improvements

- Image upload support  
- Email / push notifications  
- Priority-based complaint sorting  
- Analytics dashboard  
- Worker performance tracking  
- Mobile optimization  

---

## 👨‍💻 Author

**Prince Kumar**  
Full-Stack & ML Developer  

> Building structured systems that solve real-world campus problems.
