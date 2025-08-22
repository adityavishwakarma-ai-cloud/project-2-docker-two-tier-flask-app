
We’ll have:

1. **Web app (`app.js`)** – Node.js Express server
2. **Database init script (`init.sql`)** – Creates sample table & data

---

## 1️⃣ `web/app.js` – Node.js Web Server

```javascript
// app.js
const express = require('express');
const mysql = require('mysql');
const app = express();
const port = 8080;

// MySQL database connection
const db = mysql.createConnection({
  host: 'db',          // service name in docker-compose
  user: 'appuser',
  password: 'app123',
  database: 'appdb'
});

db.connect((err) => {
  if (err) {
    console.error('Database connection failed:', err);
  } else {
    console.log('Connected to MySQL database!');
  }
});

// Route: Home
app.get('/', (req, res) => {
  db.query('SELECT * FROM users', (err, results) => {
    if (err) {
      res.send('Error fetching data');
    } else {
      res.json(results);
    }
  });
});

app.listen(port, () => {
  console.log(`Web app running at http://localhost:${port}`);
});
```

---

### 2️⃣ `web/package.json` – Node.js Dependencies

```json
{
  "name": "two-tier-web",
  "version": "1.0.0",
  "description": "Two-tier app frontend",
  "main": "app.js",
  "scripts": {
    "start": "node app.js"
  },
  "dependencies": {
    "express": "^4.18.2",
    "mysql": "^2.18.1"
  }
}
```

---

## 3️⃣ `db/init.sql` – Database Initialization Script

```sql
-- init.sql

CREATE TABLE IF NOT EXISTS users (
    id INT AUTO_INCREMENT PRIMARY KEY,
    name VARCHAR(50) NOT NULL,
    email VARCHAR(50) NOT NULL UNIQUE
);

INSERT INTO users (name, email) VALUES
('Alice', 'alice@example.com'),
('Bob', 'bob@example.com'),
('Charlie', 'charlie@example.com');
```

---

## ✅ Folder Structure (Updated)

```
project-2-docker-twotier/
│-- README.md
│-- docker-compose.yml
│-- .gitignore
│-- web/
│   ├── app.js
│   └── package.json
│-- db/
    └── init.sql
```

---

## 📄 `.gitignore`

```gitignore
node_modules/
.env
*.log
backup/
```

---

### ⚡ How to Run End-to-End

```bash
# Build and start containers
docker-compose up -d --build

# Access web app in browser
http://localhost:8080

# Stop containers
docker-compose down
```

* You’ll see the list of users from the database in JSON format when you visit the web app.

---
