# 🎓 University Management System

A desktop **University Management System** written in **C++** with a modern **raylib** graphical interface. It manages students, courses, enrollments, prerequisites and waitlists, and every module is built on a **hand-implemented data structure** (no STL containers for the core logic). It is a hands-on showcase of Data Structures & Algorithms in a real application.

The app ships with two interfaces that share the same data: a **GUI** (dark-themed, resizable window) and a **Console Mode** (text menus).

---

## ✨ Features

### 👩‍🎓 Student Management
- Add students with ID, name, email, phone, address and password
- Prevent duplicate student IDs
- Search a student by ID
- Delete a student
- Sort students by ID
- View all students

### 📚 Course Management
- Add courses with ID, name, credits, instructor and **maximum capacity**
- Attach up to **10 prerequisite courses** to a course
- Search and drop courses
- Browse courses in sorted (in-order) sequence
- Courses are **colour-coded by credit hours** (1, 2 and 3+ credits) with an on-screen legend

### 📝 Enrollment Management
- Enroll a student in a course
- Remove an enrollment
- View all enrollments of a student
- Automatic validation of:
  - student and course existence
  - **prerequisite completion**
  - **course capacity**
  - duplicate enrollments

### 🔗 Prerequisite Checking
- Check whether a student satisfies a course's prerequisites, **including chained (nested) prerequisites**, using an explicit stack

### ⏳ Waitlist
- Add a student to a course waitlist when the course is full
- Process the waitlist: the student at the front is enrolled automatically once a seat is free and prerequisites are met

### #️⃣ Course Hash Table
- Initialize the hash table, rebuild it from the course tree, and look up courses by ID in near-constant time

### 🖥️ Interface
- Resizable GUI with a minimum window size, UI scaling, hover effects, text boxes and toast notifications
- Built-in **Console Mode** reachable from the main screen

---

## 🧠 Data Structures Used

| Module | Data Structure | Why it fits |
|---|---|---|
| Students | **Singly Linked List** | Dynamic growth, simple insertion and deletion |
| Courses | **Binary Search Tree** | Ordered storage, fast search, in-order listing |
| Enrollments | **Doubly Linked List** (head + tail) | O(1) append and easy removal from either direction |
| Prerequisite validation | **Stack** (array-based) | Depth-first walk over chained prerequisites |
| Waitlist | **Circular Queue** (capacity 10) | First-come, first-served ordering |
| Course lookup | **Hash Table** with **separate chaining** (10 buckets) | Fast lookup by course ID |

Sorting of students is done directly on the linked list.

---

## 📁 Project Structure

```
University-Management-System/
├── main.cpp          # Entire application: data structures, console mode and raylib GUI
├── main.exe          # Prebuilt Windows executable
├── ums_gui.exe       # Prebuilt Windows GUI executable
└── .vscode/          # VS Code build, debug and IntelliSense configuration
```

---

## 🛠️ Tech Stack

- **Language:** C++
- **Graphics / UI:** [raylib](https://www.raylib.com/)
- **Compiler:** g++ (MinGW / w64devkit)
- **Editor:** Visual Studio Code

---

## 🚀 Getting Started

### Option 1: Run the prebuilt app (Windows)
Download or clone the repository and run `ums_gui.exe` (or `main.exe`).

### Option 2: Build from source

**Prerequisites**
- A C++ compiler such as **w64devkit / MinGW-w64**
- The **raylib** library (source or prebuilt, compiled as a static library)

**Build with g++ (Windows)**
```bash
g++ main.cpp -o main.exe -I<path-to-raylib>/src -L<path-to-raylib>/src \
    -lraylib -lopengl32 -lgdi32 -lwinmm -static -m64
```

For example, with raylib installed at `C:/raylib`:
```bash
C:/raylib/w64devkit/bin/g++.exe main.cpp -o main.exe -IC:/raylib/raylib/src -LC:/raylib/raylib/src -lraylib -lopengl32 -lgdi32 -lwinmm -static -m64
```

**Build in VS Code**
Open the folder in VS Code and press `Ctrl + Shift + B` to run the included **"Build (raylib static, w64devkit)"** task. Adjust the raylib paths in `.vscode/tasks.json` if yours differ.

Then run:
```bash
./main.exe
```

---

## 🎮 Usage

1. Launch the app to open the **main dashboard** with six modules: *Students, Courses, Enrollments, Prerequisites, Waitlist* and *Course Hash*.
2. **Add students and courses first**. Courses can list prerequisite course IDs.
3. Go to **Enrollments** to enroll students. The system checks prerequisites and capacity for you.
4. If a course is full, use the **Waitlist** screen to queue the student, then **Process** the queue once a seat opens.
5. Use **Prerequisites** to validate a student against a course without enrolling.
6. Use **Course Hash** to initialize, rebuild and search the hash table.
7. Prefer text menus? Click **Console Mode** on the main screen.

### Console menu
```
=========== MAIN MENU ===========
1. Manage Students (SLL)
2. Manage Courses (BST)
3. Manage Enrollments (DLL)
4. Registration (Prereq Stack)
5. Waitlist (Queue)
6. Course Hash Table (Chaining)
0. Exit
=================================
```

---

## 🧩 Code Overview

- **Models:** `Student`, `Course`, `Enrollment`, `WaitlistItem`, plus node classes (`StudentNode`, `CourseNode`, `EnrollmentNode`, `CourseHashNode`)
- **Core logic:** `addStudent`, `insertCourseBST`, `addEnrollment`, `checkPrerequisitesWithStack`, `enqueueWaitlist` / `dequeueWaitlist`, `insertCourseHash` / `searchCourseHash`
- **Console UI:** `studentMenu`, `courseMenu`, `enrollmentMenu`, `prereqStackMenu`, `waitlistQueueMenu`, `hashTableMenu`
- **GUI (raylib):** `ScreenMain`, `ScreenStudents`, `ScreenCourses`, `ScreenEnroll`, `ScreenPrereq`, `ScreenWaitlist`, `ScreenHash`, with reusable `DrawButton`, `DrawTextBox` and toast helpers

---

## 👤 Author

**Abdullah Karim**
