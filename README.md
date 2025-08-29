# 🧑‍🤝‍🧑 Volunteer-Management-System
Using SQL

# Project Overview

This project is a Volunteer Management Database built using MySQL.
The aim is to manage information about volunteers, their skills, availability, location, and the type of organization they can work with.

## This project demonstrates:

Creating and loading a database.

Running SQL queries for filtering, aggregation, and matching.

Solving real-world NGO/Volunteer matching problems.

# Database Schema

## Database Name: 
Volunteer
## Table:
Volunteers

| Column Name            | Data Type            | Description                             |
| ---------------------- | -------------------- | --------------------------------------- |
| id (PK)                | INT (Auto Increment) | Unique volunteer ID                     |
| volunteer\_name        | VARCHAR(100)         | Name of volunteer                       |
| age                    | INT                  | Age of volunteer                        |
| gender                 | VARCHAR(20)          | Gender (Male/Female)                    |
| skills                 | VARCHAR(255)         | Volunteer’s skill set                   |
| availability           | VARCHAR(50)          | Availability (Weekdays, Weekends, etc.) |
| location               | VARCHAR(100)         | City/Location                           |
| type\_of\_organization | VARCHAR(100)         | NGO/Organization type                   |

# ⚙️ Setup Instructions
## Create the database:

CREATE DATABASE Volunteer;

USE Volunteer;
## Create the table:

CREATE TABLE Volunteers (
    id INT AUTO_INCREMENT PRIMARY KEY,
    volunteer_name VARCHAR(100),
    age INT,
    gender VARCHAR(20),
    skills VARCHAR(255),
    availability VARCHAR(50),
    location VARCHAR(100),
    type_of_organization VARCHAR(100)
);
## Load dataset (adjust path as needed):

LOAD DATA INFILE 'C:/Users/OneDrive/Documents/Volunteer.csv'
INTO TABLE Volunteers
FIELDS TERMINATED BY ','
ENCLOSED BY '"'
LINES TERMINATED BY '\n'
IGNORE 1 ROWS
(volunteer_name, age, gender, skills, availability, location, type_of_organization);


## 🏗️ View all volunteers
SELECT * FROM Volunteers;

## 🏗️ Volunteers available on weekends
SELECT volunteer_name, skills, location
FROM Volunteers
WHERE availability = 'Weekends';

## 🏗️ Count volunteers by gender
SELECT gender, COUNT(*) AS total_volunteers
FROM Volunteers
GROUP BY gender;

## 🏗️ Volunteers skilled in healthcare
SELECT volunteer_name, age, skills, location, availability
FROM Volunteers
WHERE skills LIKE '%Healthcare%';

## 🏗️ Volunteers by city (descending order)
SELECT location, COUNT(*) AS volunteers_count
FROM Volunteers
GROUP BY location
ORDER BY volunteers_count DESC;

## 🏗️ Match volunteers to organizations
SELECT volunteer_name, skills, type_of_organization
FROM Volunteers
WHERE (skills LIKE '%Animal%' AND type_of_organization = 'Pet and Animal Service')
   OR (skills LIKE '%Healthcare%' AND type_of_organization = 'Healthcare')
   OR (skills LIKE '%Teaching%' AND type_of_organization = 'Youth Development');
## 🏗️ Find youngest and oldest volunteers
SELECT MIN(age) AS youngest, MAX(age) AS oldest
FROM Volunteers;
## 🏗️ Volunteers with multiple skills
SELECT volunteer_name, skills
FROM Volunteers
WHERE skills LIKE '%,%';

## 🏗️ Volunteers above 30 available on weekdays
SELECT volunteer_name, age, skills, location
FROM Volunteers
WHERE age > 30 AND availability = 'Weekdays';

## 🏗️ Most common organization type
SELECT type_of_organization, COUNT(*) AS volunteers_count
FROM Volunteers
GROUP BY type_of_organization
ORDER BY volunteers_count DESC
LIMIT 1;

# 🎯 Key Learnings
Creating & loading SQL databases.

Writing filtering, grouping, and matching queries.

Handling real-world volunteer allocation problems.

# 📌 Tech Stack

Database: MySQL

Dataset: CSV/Excel

Queries: SQL
