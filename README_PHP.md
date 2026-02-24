# High School Grading System - PHP/MySQL Version

## Setup Instructions

### 1. Database Setup

1. Create MySQL database:
```bash
mysql -u root -p < database/schema_mysql.sql
```

Or import via phpMyAdmin:
- Create database named `grading_system`
- Import `database/schema_mysql.sql`

2. Update database credentials in `config/database.php`:
```php
$db_config = [
    'host' => 'localhost',
    'dbname' => 'grading_system',
    'username' => 'root',
    'password' => 'your_password',
    'charset' => 'utf8mb4'
];
```

### 2. Seed Database (Optional)

Run the seeding script to populate initial data:
```bash
php scripts/seed.php
```

This creates:
- Admin user (username: `admin`, password: `admin123`)
- Test teachers (username: `teacher1/2/3`, password: `password123`)
- Sample classes and students
- Test marks data

### 3. Web Server Configuration

#### Apache
Ensure mod_rewrite is enabled. The `.htaccess` file handles URL rewriting.

#### Nginx
Add to your server block:
```nginx
location / {
    try_files $uri $uri/ /public/$uri;
}

location /api/ {
    rewrite ^/api/(.+)$ /api/$1.php last;
}
```

### 4. PHP Configuration

Ensure PHP has:
- PDO extension enabled
- Session support enabled
- JSON support enabled

### 5. File Permissions

Make sure PHP can write to session directory and read all files.

## Default Login Credentials

- **Admin**: username `admin`, password `admin123`
- **Teachers**: username `teacher1`, `teacher2`, or `teacher3`, password `password123`
- **Students**: username `stu001`, `stu002`, etc., password `password123`

## API Endpoints

All endpoints are under `/api/`:

- `POST /api/login` - User login
- `POST /api/logout` - User logout
- `GET /api/user` - Get current user info
- `GET /api/classes` - Get all classes
- `POST /api/classes` - Create new class (admin only)
- `GET /api/subjects` - Get all subjects
- `POST /api/subjects` - Create new subject (admin only)
- `GET /api/students` - Get students (filtered by role)
- `POST /api/students` - Create new student (admin only)
- `GET /api/marks` - Get marks
- `POST /api/marks` - Create/update marks (admin/teacher)
- `GET /api/reports?studentId=X` - Get student report
- `GET /api/users/teachers` - Get all teachers (admin only)
- `POST /api/users` - Create new user (admin only)
- `GET /api/academic-years` - Get academic years

## Differences from Node.js Version

1. **Database**: SQLite → MySQL
2. **Sessions**: Express-session → PHP sessions
3. **Password Hashing**: bcryptjs → PHP password_hash/password_verify
4. **API Routing**: Express routes → PHP files with .htaccess routing
5. **Error Handling**: Express error middleware → PHP try-catch with JSON responses

## Troubleshooting

- **404 on API calls**: Check .htaccess is working and mod_rewrite is enabled
- **Database connection errors**: Verify credentials in `config/database.php`
- **Session errors**: Check PHP session configuration
- **CORS issues**: Add CORS headers if needed in PHP files

