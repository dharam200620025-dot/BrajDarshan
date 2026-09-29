const express = require('express');
const mysql = require('mysql2');
const cors = require('cors');

const app = express();
app.use(cors());
app.use(express.json());

// MySQL Database Connection (Apna password zaroor check karein)
const db = mysql.createConnection({
    host: 'localhost',
    user: 'root',
    password: '', 
    database: 'braj_darshan'
});

db.connect((err) => {
    if (err) console.error('Database connection failed:', err);
    else console.log('✅ MySQL Database Connected!');
});

// API 1: User Login (Email save karna)
app.post('/api/login', (req, res) => {
    const { email } = req.body;
    if (!email) return res.status(400).send("Email is required");

    const query = 'INSERT IGNORE INTO users (email) VALUES (?)';
    db.query(query, [email], (err, result) => {
        if (err) return res.status(500).send(err);
        res.status(200).json({ message: "Login successful", email: email });
    });
});

// API 2: Save Contribution
app.post('/api/contribute', (req, res) => {
    const { email, place_name } = req.body;
    const query = 'INSERT INTO contributions (user_email, place_name) VALUES (?, ?)';
    db.query(query, [email, place_name], (err, result) => {
        if (err) return res.status(500).send(err);
        res.status(200).json({ message: "Contribution saved!" });
    });
});

const PORT = 3000;
app.listen(PORT, () => {
    console.log(`🚀 Backend Server running at http://localhost:${PORT}`);
});
