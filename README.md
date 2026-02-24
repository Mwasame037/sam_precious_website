# Kenyan High School Grading System (8-4-4 Curriculum)

A comprehensive web-based grading system for Kenyan high schools following the 8-4-4 curriculum structure.

## Features

- **Role-based Access Control**: Admin, Class Teacher, and Student roles
- **Subject Management**: Support for compulsory and optional subjects
- **Form-based Configuration**: 11 subjects for Form 1-2, 8 subjects for Form 3-4
- **Assessment Tracking**: CAT 1, CAT 2, and End-Term examinations per term
- **KCSE Grading System**: Automatic calculation using the 12-point scale (A to E)
- **Performance Reports**: Term reports, annual reports, and mean score calculations
- **Responsive Design**: Mobile-first responsive UI

## Technology Stack

- **Backend**: Node.js + Express
- **Database**: SQLite
- **Frontend**: HTML, CSS, JavaScript (Vanilla)
- **Authentication**: Session-based

## Installation

1. **Clone or download the repository**

2. **Install dependencies**:
```bash
npm install
```

3. **Initialize the database**:
The database will be automatically created on first server start. The schema includes:
- Users (admin, class teachers, students)
- Classes (Form 1-4 with streams)
- Subjects (compulsory and optional)
- Students with admission numbers
- Marks for CAT 1, CAT 2, and End-Term exams
- Academic years and terms

4. **Start the server**:
```bash
npm start
```

Or for development with auto-reload:
```bash
npm run dev
```

5. **Access the application**:
Open your browser and navigate to `http://localhost:3000`

## Test Accounts

The system automatically seeds test data on first run:

### Admin
- **Username**: `admin`
- **Password**: `admin123`

### Class Teachers
- **Username**: `teacher1`, `teacher2`, `teacher3`
- **Password**: `password123`

### Students
- **Username**: `stu001`, `stu002`, `stu003`, etc. (lowercase admission numbers)
- **Password**: `password123`

**⚠️ Important**: Change all default passwords after first login in production!

The test data includes:
- 3 classes (Form 1A, Form 2A, Form 3B)
- 10 students across different classes
- Sample marks for 5 students across all 3 terms
- All compulsory subjects with marks

## System Structure

### Database Schema

- `users`: System users (admin, class teachers, students)
- `classes`: Form classes with streams (e.g., Form 2A, Form 3B)
- `subjects`: All available subjects with compulsory/optional flags
- `students`: Student records with admission numbers
- `student_subjects`: Subject registrations per student per term
- `marks`: Assessment marks (CAT 1, CAT 2, End-Term) with calculated grades
- `academic_years`: Academic year management
- `terms`: Term management (Term 1, 2, 3)

### User Roles

#### Admin
- Create and manage classes
- Add/edit subjects (mark as compulsory or optional)
- Register students
- Add class teachers
- View all reports and data

#### Class Teacher
- Enter marks for students in their assigned class
- View class performance
- Generate reports for their class

#### Student
- View personal results
- Access term and annual reports
- View progress over time

## Grading System

The system uses the KCSE 12-point grading scale:

| Marks (%) | Grade | Points |
|-----------|-------|--------|
| 80-100    | A     | 12     |
| 75-79     | A-    | 11     |
| 70-74     | B+    | 10     |
| 65-69     | B     | 9      |
| 60-64     | B-    | 8      |
| 55-59     | C+    | 7      |
| 50-54     | C     | 6      |
| 45-49     | C-    | 5      |
| 40-44     | D+    | 4      |
| 35-39     | D     | 3      |
| 30-34     | D-    | 2      |
| 0-29      | E     | 1      |

### Assessment Weights

- **CAT 1**: Low weight (diagnostic)
- **CAT 2**: Moderate weight
- **End-Term**: Highest weight (determines final term grade)

Total marks = CAT 1 + CAT 2 + End-Term (out of 100)

## Usage Guide

### Setting Up a New Academic Year

1. Login as Admin
2. Navigate to Reports section
3. Create a new academic year (e.g., "2024/2025")

### Adding Students

1. As Admin, go to "Manage Students"
2. Click "Add New Student"
3. Enter admission number, name, and assign to a class
4. The system automatically assigns subjects based on form level

### Entering Marks

1. As Class Teacher, go to "Enter Results"
2. Select class, academic year, term, and subject
3. Enter marks for CAT 1, CAT 2, and End-Term for each student
4. Click "Save" for each student
5. Grades and points are calculated automatically

### Generating Reports

1. Select the appropriate role dashboard
2. Navigate to "Reports" or "My Results"
3. Select academic year and term
4. View or export the report

## File Structure

```
HighSchoolGradingSystem/
├── database/
│   └── schema.sql          # Database schema definition
├── public/
│   ├── index.html          # Login page
│   ├── dashboard.html      # Main dashboard
│   ├── styles.css          # Stylesheet
│   ├── auth.js            # Authentication logic
│   └── dashboard.js       # Dashboard functionality
├── server.js              # Express server and API routes
├── package.json           # Dependencies and scripts
└── README.md             # This file
```

## API Endpoints

### Authentication
- `POST /api/login` - User login
- `POST /api/logout` - User logout
- `GET /api/user` - Get current user info

### Classes
- `GET /api/classes` - List all classes
- `POST /api/classes` - Create new class (Admin only)

### Subjects
- `GET /api/subjects` - List all subjects
- `POST /api/subjects` - Add new subject (Admin only)

### Students
- `GET /api/students` - List students (filtered by role)
- `POST /api/students` - Add new student (Admin only)

### Marks
- `GET /api/marks` - Get marks (filtered by role)
- `POST /api/marks` - Save/update marks (Admin/Class Teacher)

### Reports
- `GET /api/reports/student/:studentId` - Get student report

### Users
- `GET /api/users/teachers` - List teachers (Admin only)
- `POST /api/users` - Create new user (Admin only)

## Security Notes

- Passwords are hashed using bcryptjs
- Session-based authentication
- Role-based access control on API endpoints
- SQL injection protection using parameterized queries

## Future Enhancements

- Export reports to PDF/Excel
- Bulk mark entry via CSV upload
- Parent/guardian portal
- SMS notifications for results
- Integration with KCSE registration system
- Advanced analytics and charts
- Multi-school support

## License

This project is open source and available for educational purposes.

## Support

For issues or questions, please check the code comments or refer to the Kenyan 8-4-4 curriculum documentation.

