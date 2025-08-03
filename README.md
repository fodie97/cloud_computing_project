# 🍽️ TripMeal

**A Cloud-Native Recipe Sharing Web Application**
> 📹 **Demo Video**: https://drive.google.com/drive/u/0/folders/1Mt8jl8B6i8WvL6jO8cVZNTm_yqwXc9I_

---

## 👥 Contributors

- **Fodié Niakaté**  
- **Ali Cherifi Alaoui**

We worked together on the design, development, containerization, and deployment of the TripMeal application.

---

## 📌 Summary

1. [High-Level Description](#1-high-level-description)  
2. [File Organization and Purpose](#2-file-organization-and-purpose)  
   - [Folder: db](#21-folder-db)  
   - [Folder: web](#22-folder-web)  
   - [Root-Level Files](#23-root-level-files)  
3. [Technologies Used](#3-technologies-used)  
4. [Port Configuration](#4-port-configuration)  
5. [Explanation of `tripmeal.yml`](#5-explanation-of-tripmealyml)  
6. [Conclusion and Project Impressions](#6-conclusion-and-project-impressions)

---

## 1. High-Level Description

TripMeal is a user-friendly web platform for food lovers to explore, share, and manage recipes. It provides:

- Secure account creation and login  
- Adding, editing, and deleting recipes  
- Browsing and saving favorite recipes  
- A personalized user profile

Built with a clean UI and robust backend, TripMeal is scalable and reliable, both locally and on the cloud.

---

## 2. File Organization and Purpose

TripMeal is structured to separate concerns between frontend, backend, and DevOps components.

### 2.1 Folder: `db`

Handles the backend database.

- `Dockerfile`: Builds the MySQL container  
- `init-db.sql`: Creates schema and tables  
- `mysqld.cnf`: Custom MySQL configuration  

### 2.2 Folder: `web`

Hosts the frontend and backend logic using Flask.

#### `static/`

- `bootstrap.min.css`, `bootstrap.min.js`: UI styling and interactivity  
- `favicon.ico`: Browser icon  

#### `templates/`

- `login.html`, `register.html`, `main.html`, `newrecipe.html`, `recipes.html`, `edit_recipe.html`

#### Core Files

- `app.py`: Main Flask app  
- `dbconnect.py`: DB connection logic  
- `requirements.txt`: Python dependencies  
- `Dockerfile`: Container for the Flask app  

### 2.3 Root-Level Files

- `docker-compose.yml`: (Unused) Local orchestration  
- `tripmeal.yml`: Kubernetes deployment manifest  
- `tripmeal.env`: Environment variables

> ⚠️ _Note_: We manually built and deployed containers. While this worked, using `docker-compose` could have streamlined the process.

---

## 3. Technologies Used

### 3.1 Programming Languages

- Python (Flask backend)  
- SQL (MySQL queries)  
- HTML / CSS / JavaScript (Frontend)

### 3.2 Libraries & Frameworks

- Flask  
- Bootstrap  
- MySQL Connector

### 3.3 Database

- MySQL

### 3.4 DevOps Tools

- Docker  
- Kubernetes (GKE)  
- Google Cloud Platform (GCP)

---

## 4. Port Configuration

| Port  | Component      | Purpose                                         |
|-------|----------------|-------------------------------------------------|
| 7070  | Web (external) | Public access via Kubernetes LoadBalancer       |
| 5000  | Web (internal) | Flask listens for HTTP requests                 |
| 3306  | Database       | SQL operations from web to MySQL                |

---

## 5. Explanation of `tripmeal.yml`

### 5.1 Kubernetes Objects Overview

Manages:

- **Services** (web & DB)
- **Deployment** (frontend)
- **StatefulSet** (database)

### 5.2 Services

#### Web Service

- Type: LoadBalancer  
- Ports: `7070` → `5000`

#### Database Service

- Type: ClusterIP  
- Port: `3306`

### 5.3 Stateless Deployment (Frontend)

- Deployment of Flask web app  
- 1 replica  
- Environment variables for DB access  
- Auto-recovery on failure

### 5.4 StatefulSet Deployment (Database)

- MySQL with persistent storage  
- Volume mounted at `/var/lib/mysql`  
- Unique pod names (e.g. `db-0`)

### 5.5 Port Summary

| Port  | Used By     | Description                          |
|-------|-------------|--------------------------------------|
| 7070  | Web         | Public entry via LoadBalancer        |
| 5000  | Web         | Internal Flask application port      |
| 3306  | Database    | MySQL query handling                 |

### 5.6 Deployment Process

1. **Docker Build & Push**  
   - Frontend and DB images pushed to Google Artifact Registry  
2. **Deployment to GKE**  
   - `tripmeal.yml` applied to Kubernetes cluster  
   - External IP exposed via LoadBalancer  
3. **Result**  
   - 🎥 https://drive.google.com/drive/u/0/folders/1Mt8jl8B6i8WvL6jO8cVZNTm_yqwXc9I_

---

## 6. Conclusion and Project Impressions

This project was an enriching and rewarding experience. It allowed us to:

- Learn full-stack deployment  
- Work with Docker, Kubernetes, and GCP  
- Focus on both DevOps and user experience  

Building TripMeal helped us understand the intersection between backend infrastructure and frontend usability. We’re proud of the result and excited to apply this knowledge in real-world applications.

---
