# Zomato SQL Project

-- Creating Database Zomato 
create database Zomato;

-- Use Database Zomato
use Zomato;

-- Creating Table Customer

create table Customer
(
Customer_id int auto_increment PRIMARY KEY,
Customer_name VARCHAR(50),
reg_date DATE
);

-- Creating Table Restaurants

CREATE TABLE Restaurants (
    restaurant_id int auto_increment PRIMARY KEY,
    restaurant_name VARCHAR(100),
    city VARCHAR(50),
    opening_hours VARCHAR(50)
);

CREATE TABLE Orders (
    order_id SERIAL PRIMARY KEY,
    customer_id INTEGER NOT NULL,
    restaurant_id INTEGER NOT NULL,
    order_item VARCHAR(255),
    order_date DATE,
    order_time TIME,
    order_status VARCHAR(20),
    total_amount NUMERIC(10, 2),
    FOREIGN KEY (customer_id) REFERENCES customer(customer_id),
    FOREIGN KEY (restaurant_id) REFERENCES restaurants(restaurant_id)
);

-- Creating Table for Riders 
select * from Riders;
CREATE TABLE Riders (
    rider_id INT PRIMARY KEY,
    rider_name VARCHAR(55),
    sign_up_date DATE
);


-- Creating Table for Deliveries

CREATE TABLE deliveries (
    delivery_id INT AUTO_INCREMENT PRIMARY KEY,
    order_id BIGINT UNSIGNED NOT NULL,
    delivery_status VARCHAR(20),
    delivery_time TIME,
    rider_id INT NOT NULL,
    FOREIGN KEY (order_id) REFERENCES orders(order_id),
    FOREIGN KEY (rider_id) REFERENCES riders(rider_id)
);












