# MySQL Setup Instructions

This project has been migrated from Supabase to use a local MySQL database. Follow these steps to set up MySQL for the application.

## Prerequisites

1. Install MySQL on your system:
   - **Windows**: Download from [MySQL Official Website](https://dev.mysql.com/downloads/installer/)
   - **macOS**: `brew install mysql`
   - **Linux**: `sudo apt install mysql-server`

2. Start MySQL service:
   - **Windows**: Start the MySQL service from Services
   - **macOS**: `brew services start mysql`
   - **Linux**: `sudo systemctl start mysql`

## MySQL Configuration

1. Log in to MySQL as root:
   ```bash
   mysql -u root -p
   ```
   (Enter your root password when prompted, or press Enter if no password is set)

2. Create a database for the application:
   ```sql
   CREATE DATABASE ziya_forms;
   ```

3. (Optional) Create a dedicated user for the application:
   ```sql
   CREATE USER 'ziya_user'@'localhost' IDENTIFIED BY 'your_password_here';
   GRANT ALL PRIVILEGES ON ziya_forms.* TO 'ziya_user'@'localhost';
   FLUSH PRIVILEGES;
   ```

## Environment Configuration

Update your `.env.local` file with the correct MySQL credentials:

```env
# MySQL Database Configuration
MYSQL_HOST=localhost
MYSQL_PORT=3306
MYSQL_USER=root            # or 'ziya_user' if you created a dedicated user
MYSQL_PASSWORD=            # your MySQL password (leave empty if none)
MYSQL_DATABASE=ziya_forms

# NextAuth Configuration
NEXTAUTH_SECRET=your_nextauth_secret_here
NEXTAUTH_URL=http://localhost:5000

# Google OAuth (if you're using it)
GOOGLE_CLIENT_ID=your_google_client_id
GOOGLE_CLIENT_SECRET=your_google_client_secret
```

## Database Initialization

After configuring your environment variables, run the setup script to create the database tables:

```bash
npm run setup-db
```

## Troubleshooting

If you encounter connection issues:

1. **Access denied errors**: Verify your MySQL username and password
2. **Can't connect to MySQL**: Ensure the MySQL service is running
3. **Database doesn't exist**: Run the setup script or manually create the database

For Windows users, if you're getting "Access denied" errors:
- Make sure you're using the correct password
- You might need to reset the root password:
  ```sql
  ALTER USER 'root'@'localhost' IDENTIFIED BY 'new_password';
  ```