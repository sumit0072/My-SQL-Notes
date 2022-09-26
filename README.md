<h1>MySQL Cheat Sheet</h1>
<blockquote>Help with SQL commands to interact with a MySQL database</blockquote>

<h2>MySQL Locations</h2>
<ul>
    <li><b>Mac</b> /usr/local/mysql/bin</li>
    <li><b>Windows</b> /Program Files/MySQL/MySQL version/bin</li>
    <li><b>Xampp</b> /xampp/mysql/bin</li>
</ul>

<h2>Add mysql to your PATH</h2>

```bash
# Current Session
export PATH=${PATH}:/usr/local/mysql/bin
# Permanantly
echo 'export PATH="/usr/local/mysql/bin:$PATH"' >> ~/.bash_profile
```

<h2>Login</h2>

```bash
mysql -u root -p
```

<h2>Show Users</h2>

```sql
SELECT User, Host FROM mysql.user;
```

<h2>Create User</h2>

```sql
CREATE USER 'someuser'@'localhost' IDENTIFIED BY 'somepassword';
```

<h2>Grant All Priveleges On All Databases</h2>

```sql
GRANT ALL PREVILEGES ON * . * TO 'someuser'@'localhost';
FLUSH PREVILEGES;
```

<h2>Show Grants</h2>

```sql
SHOW GRANTS FOR 'someuser'@'localhost';
```

<h2>Remove Grants</h2>

```sql
REVOKE ALL PREVILEGES, GRANT OPTION FROM 'someuser'@'localhost';
```

<h2>Delete User</h2>

```sql
DROP USER 'someuser'@'localhost';
```

<h2>Exit</h2>

```sql
exit;
```

<h2>Show Databases</h2>

```sql
SHOW DATABASES;
```

<h2>Create Database</h2>

```sql
CREATE DATABASE academy;
```

<h2>Delete Database</h2>

```sql
DROP DATABASE academy;
```

<h2>Select Database</h2>

```sql
USE academy;
```

<h2>Create Table</h2>

```sql
CREATE TABLE users(
id INT AUTO_INCREMENT,
first_name VARCHAR(100),
last_name VARCHAR(100),
email VARCHAR(50),
password VARCHAR(20),
location VARCHAR(100),
sport VARCHAR(100),
is_admin TINYINT(1),
register_date DATETIME,
PRIMARY KEY(id)
);
```

<h2>Delete / Drop Table</h2>

```sql
DROP TABLE tablename;
```

<h2>Show Tables</h2>

```sql
SHOW TABLES;
```

<h2>Insert Row / Record</h2>

```sql
INSERT INTO users (first_name, last_name, email, password, location, sport, is_admin, register_date) values ('Sumit', 'Mohod', 'sumit@gmail.com', '12345678', 'Banglore', 'Datacience', 1, now()); 
```

<h2>Insert Multiple Rows</h2>

```sql
INSERT INTO users (first_name, last_name, email, password, location, sport, is_admin, register_date) values ('Virat', 'Kohli', 'virat@gmail.com', '123456', 'New Delhi', 'Cricket', 0, now()), ('Roger', 'Federer', 'roger@gmail.com', '123456', 'Basel', 'Tennis', 0, now()), ('Cristiano', 'Ronaldo', 'cristiano@gmail.com', '123456', 'Funchal', 'Football', 0, now()), ('Magnus', 'Carlsen', 'magnus@gmail.com', '123456', 'Norway', 'Chess', 0, now()), ('Rohit', 'Sharma', 'rohit@gmail.com', '123456', 'Mumbai', 'Cricket', 0, now());
```

<h2>Select</h2>

```sql
SELECT * FROM users;
SELECT firstname, last_name FROM users;
```

<h2>Where Clause</h2>

```sql
SELECT * FROM users WHERE location = 'Basel';
SELECT * FROM users WHERE location = 'Funchal' AND sport = 'Football';
SELECT * FROM users WHERE is_admin = 1;
SELECT * FROM users WHERE is_admin < 1;
```

<h2>Delete Row</h2>

```sql
DELETE  FROM users WHERE id = 6;
```

<h2>Update Row</h2>

```sql
UPDATE users SET email = 'mcarlsen@gmail.com' WHERE id = 5; 
```

<h2>Add New Column</h2>

```sql
ALTER TABLE users ADD age VARCHAR(3);
```

<h2>Modify Column</h2>

```sql
ALTER TABLE users MODIFY COLUMN age INT(3);
```

<h2>Order By (Sort)</h2>

```sql
SELECT * FROM users ORDER BY last_name ASC;
SELECT * FROM users ORDER BY last_name DESC; 
```

<h2>Concatenate Columns</h2>

```sql
SELECT CONCAT(first_name, ' ', last_name) AS 'Name', sport FROM users;
```

<h2>Select Distinct Rows</h2>

```sql
SELECT DISTINCT location FROM users;
```

<h2>Between (Select Range)</h2>

```sql
SELECT * FROM users where age BETWEEN 20 AND 30; 
```

<h2>Like (Searching)</h2>

```sql
SELECT * FROM users WHERE sport LIKE 'T%';
SELECT * FROM users WHERE sport LIKE 'Cri%';
SELECT * FROM users WHERE sport LIKE '%s';
SELECT * FROM users WHERE sport LIKE '%oo%';
```

<h2>Not Like</h2>

```sql
SELECT * FROM users WHERE sport NOT LIKE 'C%'; 
```

<h2>IN</h2>

```sql
SELECT * FROM users WHERE sport IN ('Football', 'Tennis');
```

<h2>Create & Remove Index</h2>

```sql
CREATE INDEX LIndex ON users(location);
DROP INDEX LIndex ON users;
```

<h2>New Table With Foreign Key (Posts)</h2>

```sql
CREATE TABLE posts(
id INT AUTO_INCREMENT,
user_id INT,
title VARCHAR(100),
body TEXT,
publish_date DATETIME DEFAULT CURRENT_TIMESTAMP,
PRIMARY KEY (id), 
FOREIGN KEY (user_id) REFERENCES user (id) 
);
```

<h2>Add Data to Posts Table</h2>

```sql
INSERT INTO posts(user_id, title, body) values (1, 'Post One', 'This is post one'),(3, 'Post Two', 'This is post two'),(1, 'Post Three', 'This is post three'),(2, 'Post Four', 'This is post four'),(5, 'Post Five', 'This is post five'),(4, 'Post Six', 'This is post six'),(2, 'Post Seven', 'This is post seven'),(1, 'Post Eight', 'This is post eight'),(3, 'Post Nine', 'This is post none'),(4, 'Post Ten', 'This is post ten');
```

<h2>INNER JOIN</h2>

```sql
SELECT users.first_name, users.last_name, posts.title, posts.publish_date
FROM users INNER JOIN posts
ON users.id = posts.user_id
ORDER BY posts.title;
```

<h2>New Table With 2 Foreign Keys</h2>

```sql
CREATE TABLE comments(
id INT AUTO_INCREMENT,
post_id INT,
user_id INT,
body TEXT,
publish_date DATETIME DEFAULT CURRENT_TIMESTAMP,
PRIMARY KEY (id),
FOREIGN KEY (user_id) REFERENCES users(id),
FOREIGN KEY (post_id) REFERENCES posts(id)
);
```

<h2>Add Data to Comments Table</h2>

```sql
INSERT INTO comments(post_id, user_id, body) VALUES (1, 3, 'This is comment one'),(2, 1, 'This is comment two'),(5, 3, 'This is comment three'),(2, 4, 'This is comment four'),(1, 2, 'This is comment five'),(3, 1, 'This is comment six'),(3, 2, 'This is comment six'),(5, 4, 'This is comment seven'),(2, 3, 'This is comment seven');
```

<h2>Left Join</h2>

```sql
SELECT comments.body, posts.title
FROM comments
LEFT JOIN posts ON posts.id = comments.post_id
ORDER BY posts.title;
```

<h2>Join Multiple Tables</h2>

```sql
SELECT comments.body, posts.title, users.first_name, users.last_name
FROM comments
INNER JOIN posts ON posts.id = comments.post_id
INNER JOIN users ON users.id = comments.user_id
ORDER BY posts.title;
```

<h2>Aggregate Functions</h2>

```sql
SELECT COUNT(id) FROM users;
SELECT MAX(age) FROM users;
SELECT MIN(age) FROM users;
SELECT SUM(age) FROM users;
SELECT UCASE(first_name), LCASE(last_name) FROM users;
```

<h2>Group By</h2>

```sql
SELECT age, COUNT(age) FROM users GROUP BY age;
SELECT age, COUNT(age) FROM users WHERE age > 30 GROUP BY age;
SELECT age, COUNT(age) FROM users GROUP BY age HAVING COUNT(age) >= 40; 
```