# 🐘 Ultimate PostgreSQL Commands Guide: From Beginner to Professional

## 📘 Table of Contents
1. [Introduction](#introduction)
2. [Installation](#installation)
3. [Connection and Server Management](#connection-and-server-management)
4. [Database Management](#database-management)
5. [Schema Management](#schema-management)
6. [Table Operations](#table-operations)
7. [Data Manipulation](#data-manipulation)
8. [Querying Data](#querying-data)
9. [Indexing](#indexing)
10. [User and Role Management](#user-and-role-management)
11. [Performance Optimization](#performance-optimization)
12. [Backup and Recovery](#backup-and-recovery)
13. [Advanced Techniques](#advanced-techniques)
14. [Troubleshooting](#troubleshooting)
15. [Best Practices](#best-practices)

## 📍 Introduction

PostgreSQL is a powerful, open-source relational database management system known for its reliability, feature robustness, and performance.

## 🔧 Installation

### Linux (Ubuntu/Debian)
```bash
# Install PostgreSQL
sudo apt update
sudo apt install postgresql postgresql-contrib

# Start PostgreSQL service
sudo systemctl start postgresql
sudo systemctl enable postgresql
```

### macOS (using Homebrew)
```bash
# Install PostgreSQL
brew install postgresql

# Start PostgreSQL service
brew services start postgresql
```

### Windows
- Download installer from official PostgreSQL website
- Run the installer
- Follow installation wizard
- Set postgres user password

## 🔌 Connection and Server Management

### Connecting to PostgreSQL
```bash
# Connect as default postgres user
psql

# Connect to specific database
psql -d database_name

# Connect with specific user
psql -U username -d database_name

# Connect with host and port
psql -h hostname -p 5432 -U username -d database_name
```

### Server-Level Commands
```sql
-- List all databases
\l

-- List all tables
\dt

-- List all schemas
\dn

-- Show database connections
\conninfo

-- Change connection password
\password

-- Quit psql
\q
```

## 🗃️ Database Management

### Creating and Managing Databases
```sql
-- Create a new database
CREATE DATABASE database_name;

-- Create database with specific owner
CREATE DATABASE database_name OWNER username;

-- Drop a database
DROP DATABASE database_name;

-- Rename a database
ALTER DATABASE old_name RENAME TO new_name;
```

## 📊 Schema Management

### Schema Operations
```sql
-- Create a new schema
CREATE SCHEMA schema_name;

-- Create schema with authorization
CREATE SCHEMA schema_name AUTHORIZATION username;

-- Drop a schema
DROP SCHEMA schema_name;

-- Create table in specific schema
CREATE TABLE schema_name.table_name (
    column1 datatype,
    column2 datatype
);
```

## 🗂️ Table Operations

### Creating Tables
```sql
-- Basic table creation
CREATE TABLE users (
    id SERIAL PRIMARY KEY,
    username VARCHAR(50) UNIQUE NOT NULL,
    email VARCHAR(100) UNIQUE NOT NULL,
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);

-- Table with constraints
CREATE TABLE products (
    id SERIAL PRIMARY KEY,
    name VARCHAR(100) NOT NULL,
    price DECIMAL(10,2) CHECK (price > 0),
    category VARCHAR(50)
);
```

### Altering Tables
```sql
-- Add a column
ALTER TABLE table_name ADD COLUMN column_name datatype;

-- Modify column type
ALTER TABLE table_name ALTER COLUMN column_name TYPE new_datatype;

-- Rename a column
ALTER TABLE table_name RENAME COLUMN old_name TO new_name;

-- Drop a column
ALTER TABLE table_name DROP COLUMN column_name;

-- Add constraint
ALTER TABLE table_name ADD CONSTRAINT constraint_name UNIQUE(column_name);
```

## 📝 Data Manipulation

### Inserting Data
```sql
-- Basic insert
INSERT INTO users (username, email) 
VALUES ('johndoe', 'john@example.com');

-- Insert multiple rows
INSERT INTO products (name, price, category)
VALUES 
    ('Laptop', 999.99, 'Electronics'),
    ('Smartphone', 599.99, 'Electronics');
```

### Updating Data
```sql
-- Update specific rows
UPDATE users 
SET email = 'newemail@example.com' 
WHERE username = 'johndoe';

-- Conditional update
UPDATE products
SET price = price * 1.1
WHERE category = 'Electronics';
```

### Deleting Data
```sql
-- Delete specific rows
DELETE FROM users WHERE id = 5;

-- Truncate entire table
TRUNCATE TABLE table_name;
```

## 🔍 Querying Data

### Basic Queries
```sql
-- Select all columns
SELECT * FROM users;

-- Select specific columns
SELECT username, email FROM users;

-- Filtering with WHERE
SELECT * FROM products 
WHERE price > 500 AND category = 'Electronics';

-- Sorting
SELECT * FROM users 
ORDER BY created_at DESC;

-- Limit results
SELECT * FROM products 
LIMIT 10;
```

### Advanced Querying
```sql
-- Joins
SELECT u.username, o.order_date 
FROM users u
JOIN orders o ON u.id = o.user_id;

-- Aggregations
SELECT category, 
       AVG(price) as avg_price, 
       COUNT(*) as product_count 
FROM products 
GROUP BY category;

-- Subqueries
SELECT * FROM products 
WHERE price > (
    SELECT AVG(price) FROM products
);
```

## 🚀 Indexing

### Creating Indexes
```sql
-- Basic index
CREATE INDEX idx_username ON users(username);

-- Unique index
CREATE UNIQUE INDEX idx_email ON users(email);

-- Composite index
CREATE INDEX idx_name_price ON products(name, price);
```

## 👥 User and Role Management

### Creating Users and Roles
```sql
-- Create a role
CREATE ROLE app_user WITH LOGIN PASSWORD 'secure_password';

-- Grant privileges
GRANT SELECT, INSERT ON users TO app_user;

-- Create user with specific privileges
CREATE USER app_admin WITH 
    LOGIN 
    PASSWORD 'admin_password'
    CREATEDB
    CREATEROLE;
```

## 🛠️ Performance Optimization

### Analyzing and Explaining Queries
```sql
-- Analyze table statistics
ANALYZE users;

-- Explain query plan
EXPLAIN ANALYZE 
SELECT * FROM products 
WHERE price > 500;
```

## 💾 Backup and Recovery

### Backup Methods
```bash
# Backup entire database
pg_dump database_name > backup.sql

# Backup specific schema
pg_dump -n schema_name database_name > schema_backup.sql

# Restore database
psql database_name < backup.sql
```

## 🔬 Advanced Techniques

### JSON and JSONB Support
```sql
-- Create table with JSON column
CREATE TABLE user_preferences (
    id SERIAL PRIMARY KEY,
    preferences JSONB
);

-- Insert JSON data
INSERT INTO user_preferences (preferences)
VALUES ('{"theme": "dark", "notifications": true}');

-- Query JSON
SELECT preferences->'theme' FROM user_preferences;
```

## 🚨 Troubleshooting

### Common Issues
- Connection problems
- Permission errors
- Performance bottlenecks
- Disk space issues

## 📋 Best Practices

1. Use appropriate data types
2. Create indexes strategically
3. Use transactions for complex operations
4. Regularly update statistics
5. Implement proper access controls
6. Use connection pooling
7. Monitor and optimize queries

## 📚 Learning Resources
- [Official PostgreSQL Documentation](https://www.postgresql.org/docs/)
- [PostgreSQL Tutorial](https://www.postgresqltutorial.com/)
- [PostgreSQL Exercises](https://pgexercises.com/)

## 🤝 Contribution
Contributions and suggestions are welcome!

## 📄 License
[Specify your license]

---

**Pro Tip:** Mastering PostgreSQL is a journey. Practice consistently and never stop learning!