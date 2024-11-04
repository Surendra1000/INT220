# INT220
# SmartFridge Project

Welcome to the SmartFridge project! This project helps users manage food inventory, track expiration dates, get recipe suggestions, and more. Follow the instructions below to set up and run the project.

## Project Setup

### Prerequisites

- PHP and a server environment like [XAMPP](https://www.apachefriends.org/) or [WAMP](https://www.wampserver.com/).
- MySQL or MariaDB for database management.
- Basic knowledge of SQL for setting up tables and inserting initial data.

### Installation

1. **Clone the repository:**
   ```bash
   git clone https://github.com/yourusername/smartfridge.git
   ```

2. **Navigate to the project directory:**
   ```bash
   cd smartfridge
   ```

3. **Set up the database:**

   - Open your database management tool (phpMyAdmin, MySQL Workbench, etc.).
   - Create a new database named `smartfridge` (or another name if you prefer, but update your configuration accordingly).

4. **Create the required tables in the `smartfridge` database:**

   Run the following SQL commands to create the necessary tables:

   ```sql
   -- Table for admin users
   CREATE TABLE admin (
       id INT AUTO_INCREMENT PRIMARY KEY,
       username VARCHAR(50) NOT NULL,
       password VARCHAR(255) NOT NULL
   );

   -- Table for user feedback
   CREATE TABLE feedback (
       id INT AUTO_INCREMENT PRIMARY KEY,
       name VARCHAR(100) NOT NULL,
       emailid VARCHAR(100) NOT NULL,
       feedback TEXT NOT NULL
   );

   -- Table for nutrition details
   CREATE TABLE nutrition (
       id INT AUTO_INCREMENT PRIMARY KEY,
       recipe_id INT NOT NULL,
       carbohydrate FLOAT,
       fat FLOAT,
       protein FLOAT,
       calories FLOAT,
       FOREIGN KEY (recipe_id) REFERENCES recipes(id) ON DELETE CASCADE
   );

   -- Table for recipes
   CREATE TABLE recipes (
       id INT AUTO_INCREMENT PRIMARY KEY,
       name VARCHAR(255) NOT NULL,
       ingredients TEXT NOT NULL,
       instructions TEXT NOT NULL,
       origin VARCHAR(50),
       is_veg BOOLEAN,
       is_approved BOOLEAN DEFAULT 0
   );

   -- Table for submitted recipes (awaiting approval)
   CREATE TABLE submitted_recipes (
       id INT AUTO_INCREMENT PRIMARY KEY,
       name VARCHAR(255) NOT NULL,
       ingredients TEXT NOT NULL,
       instructions TEXT NOT NULL,
       origin VARCHAR(50),
       is_veg BOOLEAN,
       user_id INT,
       is_approved BOOLEAN DEFAULT 0
   );
   ```

5. **Configure the database connection:**
   
   Open `includes/db_connect.php` and update the database credentials if needed:

   ```php
   <?php
   $servername = "localhost"; // Database host
   $username = "root";        // Database username
   $password = "";            // Database password
   $dbname = "smartfridge";   // Your database name

   // Create a connection
   $conn = new mysqli($servername, $username, $password, $dbname);

   // Check the connection
   if ($conn->connect_error) {
       die("Connection failed: " . $conn->connect_error);
   }
   ?>
   ```

6. **Run the project:**

   - Start your server (e.g., XAMPP or WAMP).
   - Access the project in your browser by navigating to `http://localhost/smartfridge` (or the directory where you installed it).

---

### Features

- **Admin Dashboard:** Approve or reject submitted recipes, view user feedback, and manage content.
- **User Interactions:** Users can submit recipes, view recipe suggestions, and provide feedback.
- **Nutrition Tracking:** Each recipe has nutrition information including calories, protein, carbohydrates, and fats.
