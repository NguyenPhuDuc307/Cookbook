# SQL Queries Cơ bản

## Vấn đề
Làm thế nào để truy vấn, thêm, sửa, và xóa dữ liệu trong cơ sở dữ liệu SQL?

## Giải pháp
Sử dụng các câu lệnh SQL cơ bản: SELECT, INSERT, UPDATE, DELETE để thao tác với dữ liệu.

## Ví dụ

### Tạo bảng (CREATE TABLE)
```sql
-- Tạo bảng users
CREATE TABLE users (
    id INT PRIMARY KEY AUTO_INCREMENT,
    name VARCHAR(100) NOT NULL,
    email VARCHAR(100) UNIQUE NOT NULL,
    age INT,
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);

-- Tạo bảng posts
CREATE TABLE posts (
    id INT PRIMARY KEY AUTO_INCREMENT,
    user_id INT,
    title VARCHAR(200) NOT NULL,
    content TEXT,
    published BOOLEAN DEFAULT FALSE,
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    FOREIGN KEY (user_id) REFERENCES users(id)
);
```

### SELECT - Truy vấn dữ liệu
```sql
-- Lấy tất cả columns
SELECT * FROM users;

-- Lấy columns cụ thể
SELECT name, email FROM users;

-- WHERE - Lọc dữ liệu
SELECT * FROM users WHERE age > 25;
SELECT * FROM users WHERE name LIKE 'Nguyễn%';

-- ORDER BY - Sắp xếp
SELECT * FROM users ORDER BY age DESC;
SELECT * FROM users ORDER BY name ASC, age DESC;

-- LIMIT - Giới hạn kết quả
SELECT * FROM users LIMIT 10;
SELECT * FROM users LIMIT 10 OFFSET 20;

-- DISTINCT - Loại bỏ trùng lặp
SELECT DISTINCT age FROM users;

-- Aggregate Functions
SELECT COUNT(*) FROM users;
SELECT AVG(age) FROM users;
SELECT MAX(age), MIN(age) FROM users;
SELECT SUM(age) FROM users;

-- GROUP BY
SELECT age, COUNT(*) as count 
FROM users 
GROUP BY age;

-- HAVING - Lọc sau GROUP BY
SELECT age, COUNT(*) as count 
FROM users 
GROUP BY age 
HAVING count > 5;
```

### INSERT - Thêm dữ liệu
```sql
-- Thêm một record
INSERT INTO users (name, email, age) 
VALUES ('Nguyễn Văn A', 'a@example.com', 25);

-- Thêm nhiều records
INSERT INTO users (name, email, age) VALUES
    ('Trần Thị B', 'b@example.com', 30),
    ('Lê Văn C', 'c@example.com', 28),
    ('Phạm Thị D', 'd@example.com', 22);

-- Thêm với một số columns (columns khác dùng default)
INSERT INTO users (name, email) 
VALUES ('Hoàng Văn E', 'e@example.com');
```

### UPDATE - Cập nhật dữ liệu
```sql
-- Cập nhật một record
UPDATE users 
SET age = 26 
WHERE id = 1;

-- Cập nhật nhiều columns
UPDATE users 
SET name = 'Nguyễn Văn A (Updated)', 
    age = 27 
WHERE id = 1;

-- Cập nhật nhiều records
UPDATE users 
SET age = age + 1 
WHERE age < 30;

-- ⚠️ CẢNH BÁO: Không có WHERE sẽ update tất cả
UPDATE users SET age = 30;  -- Cẩn thận!
```

### DELETE - Xóa dữ liệu
```sql
-- Xóa một record
DELETE FROM users WHERE id = 1;

-- Xóa nhiều records
DELETE FROM users WHERE age < 18;

-- ⚠️ CẢNH BÁO: Không có WHERE sẽ xóa tất cả
DELETE FROM users;  -- Cẩn thận!

-- TRUNCATE - Xóa tất cả nhanh hơn
TRUNCATE TABLE users;
```

### JOIN - Kết hợp bảng
```sql
-- INNER JOIN - Lấy records có trong cả 2 bảng
SELECT users.name, posts.title 
FROM users
INNER JOIN posts ON users.id = posts.user_id;

-- LEFT JOIN - Lấy tất cả users, kể cả không có posts
SELECT users.name, posts.title 
FROM users
LEFT JOIN posts ON users.id = posts.user_id;

-- RIGHT JOIN - Lấy tất cả posts, kể cả không có user
SELECT users.name, posts.title 
FROM users
RIGHT JOIN posts ON users.id = posts.user_id;

-- Multiple JOINs
SELECT u.name, p.title, c.content
FROM users u
INNER JOIN posts p ON u.id = p.user_id
INNER JOIN comments c ON p.id = c.post_id;
```

### Subqueries - Truy vấn con
```sql
-- Subquery trong WHERE
SELECT * FROM users 
WHERE age > (SELECT AVG(age) FROM users);

-- Subquery với IN
SELECT * FROM users 
WHERE id IN (SELECT user_id FROM posts WHERE published = TRUE);

-- Subquery trong SELECT
SELECT 
    name,
    (SELECT COUNT(*) FROM posts WHERE user_id = users.id) as post_count
FROM users;
```

### Indexes - Tăng tốc truy vấn
```sql
-- Tạo index
CREATE INDEX idx_email ON users(email);
CREATE INDEX idx_age_name ON users(age, name);

-- Xóa index
DROP INDEX idx_email ON users;
```

## Lưu ý

**Best Practices:**
- **Luôn dùng WHERE** khi UPDATE hoặc DELETE để tránh sửa/xóa nhầm
- **Test query với SELECT** trước khi UPDATE/DELETE
- **Sử dụng transactions** cho multiple operations
- **Tạo indexes** cho columns hay search
- **Tránh SELECT *** trong production, chỉ lấy columns cần thiết
- **Sử dụng prepared statements** để tránh SQL injection

**Performance:**
- Indexes giúp tăng tốc SELECT nhưng làm chậm INSERT/UPDATE
- LIMIT kết quả khi có thể
- Tránh SELECT * với bảng lớn
- Sử dụng EXPLAIN để analyze query performance

**Security:**
```sql
-- ❌ KHÔNG an toàn (SQL Injection)
query = "SELECT * FROM users WHERE email = '" + user_input + "'";

-- ✅ An toàn (Prepared Statement)
-- Python example
cursor.execute("SELECT * FROM users WHERE email = %s", (user_input,))
```

**Transactions:**
```sql
START TRANSACTION;

INSERT INTO users (name, email) VALUES ('Test', 'test@example.com');
UPDATE users SET age = 25 WHERE name = 'Test';

-- Nếu mọi thứ OK
COMMIT;

-- Nếu có lỗi
ROLLBACK;
```

**Common Pitfalls:**
- Quên WHERE clause → update/delete tất cả
- N+1 query problem → dùng JOIN thay vì multiple queries
- Không sử dụng indexes → slow queries
- SQL injection vulnerabilities → dùng prepared statements

## Tham khảo
- [W3Schools SQL Tutorial](https://www.w3schools.com/sql/)
- [MySQL Documentation](https://dev.mysql.com/doc/)
- [PostgreSQL Tutorial](https://www.postgresqltutorial.com/)
- [SQL Bolt - Interactive Tutorial](https://sqlbolt.com/)
