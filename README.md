# Zomato SQL Project




This project models a simplified Zomato-like food delivery platform using MySQL. It includes schema creation, data relationships, and SQL queries to perform analysis and insights.

---


## 🏗️ Database Schema

### 'Create Database'

``` Create Database Zomato_DB; ```

### 'Use Database'

``` Use Zomato_DB ```

### 1. `Customer`
```sql
CREATE TABLE Customer (
    Customer_id INT AUTO_INCREMENT PRIMARY KEY,
    Customer_name VARCHAR(50),
    reg_date DATE
);
```

### 2. `Restaurants`
```sql
CREATE TABLE Restaurants (
    restaurant_id INT AUTO_INCREMENT PRIMARY KEY,
    restaurant_name VARCHAR(100),
    city VARCHAR(50),
    opening_hours VARCHAR(50)
);
```

### 3. `Orders`
```sql
CREATE TABLE Orders (
    order_id SERIAL PRIMARY KEY,
    customer_id INT NOT NULL,
    restaurant_id INT NOT NULL,
    order_item VARCHAR(255),
    order_date DATE,
    order_time TIME,
    order_status VARCHAR(20),
    total_amount NUMERIC(10,2),
    FOREIGN KEY (customer_id) REFERENCES Customer(Customer_id),
    FOREIGN KEY (restaurant_id) REFERENCES Restaurants(restaurant_id)
);
```

### 4. `Riders`
```sql
CREATE TABLE Riders (
    rider_id INT PRIMARY KEY,
    rider_name VARCHAR(55),
    sign_up_date DATE
);
```

### 5. `Deliveries`
```sql
CREATE TABLE deliveries (
    delivery_id INT AUTO_INCREMENT PRIMARY KEY,
    order_id BIGINT UNSIGNED NOT NULL,
    delivery_status VARCHAR(20),
    delivery_time TIME,
    rider_id INT NOT NULL,
    FOREIGN KEY (order_id) REFERENCES Orders(order_id),
    FOREIGN KEY (rider_id) REFERENCES Riders(rider_id)
);
```

---

## 📊 Questions Related to Projects

- **Retrieve All Customer Names**
```sql
SELECT * FROM Customer;
```

- **List all restaurants where the city is Mumbai**
```sql
SELECT * FROM Restaurants WHERE city = 'Mumbai';
```

- **Find restaurants that open before noon**
```sql
SELECT * FROM Orders
WHERE order_date >= DATE_SUB(CURRENT_DATE(), INTERVAL 1 MONTH);
```

- **Find the top 5 customers who have spent the most**
```sql
SELECT customer_id, SUM(total_amount) AS total_spent
FROM Orders
GROUP BY customer_id
ORDER BY total_spent DESC
LIMIT 5;
```

- **Find the top 3 restaurants with the highest total revenue from delivered orders**
```sql
SELECT r.restaurant_name, SUM(o.total_amount) AS total_revenue
FROM Restaurants r
JOIN Orders o ON r.restaurant_id = o.restaurant_id
JOIN Deliveries d ON o.order_id = d.order_id
WHERE d.delivery_status = 'Delivered'
GROUP BY r.restaurant_id
ORDER BY total_revenue DESC
LIMIT 3;
```

---

## 🧠 Author

**Rahul Narode**  
🎥 YouTube: [@codingwithrahul5600](https://youtube.com/@codingwithrahul5600)  
🔗 LinkedIn: [rahul-narode](https://www.linkedin.com/in/rahul-narode-3039a6212)

---

## 🛠️ Technologies Used

- MySQL
- GitHub
- CSV Data Manipulation
- SQL Joins & Aggregates











