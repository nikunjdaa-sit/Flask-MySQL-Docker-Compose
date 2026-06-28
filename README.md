# Flask-MySQL-Docker-Compose
This project demonstrates how to containerize a Python Flask web application with a MySQL database using Docker and Docker Compose. The application runs in separate containers, making it easy to set up, deploy, and maintain across different environments.

# 🐳 Flask + MySQL Multi-Container Application using Docker Compose

## 📌 Project Overview

This project demonstrates how to containerize a **Python Flask web application** and a **MySQL database** using **Docker** and **Docker Compose**.

Instead of installing Python, Flask, and MySQL directly on the host machine, each service runs inside its own Docker container. Docker Compose manages both containers and creates a private network so they can communicate securely.

# 🚀 Technologies Used

| Technology     | Version |
| -------------- | ------- |
| Python         | 3.12    |
| Flask          | 3.0.3   |
| MySQL          | 8.0     |
| Docker         | Latest  |
| Docker Compose | Latest  |

---

# 📂 Project Structure

```text
flask-mysql-project/
│
├── app.py
├── requirements.txt
├── Dockerfile
├── docker-compose.yml
├── .dockerignore
└── README.md
```

---

# 🏗️ Project Architecture
![image link](https://github.com/nikunjdaa-sit/Flask-MySQL-Docker-Compose/blob/78bfe09e92b95252108bb447bf133ff39301e8c1/flask_mysql_docker_architecture%20(1).png)

# 📄 File Description

## app.py

Main Flask application. It connects to the MySQL database, creates a table if it doesn't exist, inserts a sample record, and retrieves all records.

```python
from flask import Flask
import mysql.connector
import time

app = Flask(__name__)

def connect():
    while True:
        try:
            conn = mysql.connector.connect(
                host="db",
                user="root",
                password="password",
                database="mydatabase"
            )
            return conn
        except:
            print("Waiting for MySQL...")
            time.sleep(5)

@app.route("/")
def home():
    conn = connect()
    cursor = conn.cursor()

    cursor.execute("""
        CREATE TABLE IF NOT EXISTS users(
            id INT AUTO_INCREMENT PRIMARY KEY,
            name VARCHAR(100)
        )
    """)

    cursor.execute("INSERT INTO users(name) VALUES('Abhishek')")
    conn.commit()

    cursor.execute("SELECT * FROM users")
    data = cursor.fetchall()

    cursor.close()
    conn.close()

    return str(data)

if __name__ == "__main__":
    app.run(host="0.0.0.0", port=5000)
```

---

## requirements.txt

Contains all Python dependencies required by the application.

Example:

```text
Flask==3.0.3
mysql-connector-python==9.0.0
```

Docker automatically installs these packages while building the image.

---

## Dockerfile

Docker instructions used to build the Flask image.

```dockerfile
FROM python:3.12-slim

WORKDIR /app

COPY requirements.txt .

RUN pip install --no-cache-dir -r requirements.txt

COPY . .

CMD ["python","app.py"]
```

---

## docker-compose.yml

Creates and manages multiple containers.

Services included:

* Flask
* MySQL

Docker Compose automatically creates a network so both containers can communicate.

---

## .dockerignore

Ignores unnecessary files while building the Docker image.

Example:

```text
__pycache__
*.pyc
```

---

# ⚙️ How Docker Works in This Project

## Step 1

Docker reads the Dockerfile.

↓

## Step 2

Downloads the Python image.

↓

## Step 3

Installs Flask and MySQL Connector.

↓

## Step 4

Copies project files into the image.

↓

## Step 5

Builds the Flask Docker image.

↓

## Step 6

Docker Compose downloads the MySQL image.

↓

## Step 7

Docker Compose creates a private network.

↓

## Step 8

Both containers start.

↓

## Step 9

Flask connects to MySQL using the hostname:

```python
host="db"
```

---

# ▶️ How to Run the Project

## Clone Repository

```bash
cd flask-mysql-project
```

---

## Build Images

```bash
docker compose build
```

---

## Start Containers

```bash
docker compose up
```

---

## Open Browser

```
http://localhost:5000
```

Expected Output:

```text
[(1, 'Abhishek')]
```

---

## Stop Containers

```bash
docker compose down
```

---

# 📌 Docker Commands Used

## Build

```bash
docker compose build
```

Builds the Flask image.

---

## Run

```bash
docker compose up
```

Starts Flask and MySQL together.

---

## Stop

```bash
docker compose down
```

Stops and removes containers.

---

## List Running Containers

```bash
docker ps
```

---

## List Docker Images

```bash
docker images
```

---

# 🐳 Docker Concepts Used

* Docker Image
* Docker Container
* Dockerfile
* Docker Compose
* Docker Networking
* Environment Variables
* Port Mapping
* Build Context
* Container Communication

---

# 💡 Key Learning Outcomes

After completing this project, I learned:

* How to build Docker images
* How Docker containers work
* How Docker Compose manages multiple services
* How Flask communicates with MySQL
* How Docker networking works
* How environment variables simplify configuration
* How to containerize a backend application

---

# 🔍 Common Errors

### Dockerfile cannot be empty

**Cause**

Dockerfile is empty or not saved.

**Solution**

Save the Dockerfile and rebuild.

---

### requirements.txt not found

**Cause**

Wrong project directory.

**Solution**

Navigate to the correct folder before running Docker commands.

---

### MySQL Connection Failed

**Cause**

Database container is still starting.

**Solution**

Wait a few seconds or restart using:

```bash
docker compose up
```
# 📷 Screenshots
|Docker Build|
![image link](https://github.com/nikunjdaa-sit/Flask-MySQL-Docker-Compose/blob/78bfe09e92b95252108bb447bf133ff39301e8c1/Docker-build.png)

|Docker Compose|
![image link](https://github.com/nikunjdaa-sit/Flask-MySQL-Docker-Compose/blob/78bfe09e92b95252108bb447bf133ff39301e8c1/Docker-compose.png)

|Docker Desktop|
![imake link](https://github.com/nikunjdaa-sit/Flask-MySQL-Docker-Compose/blob/78bfe09e92b95252108bb447bf133ff39301e8c1/Docker-desktop.png)

|Docker Images|
![image link](https://github.com/nikunjdaa-sit/Flask-MySQL-Docker-Compose/blob/78bfe09e92b95252108bb447bf133ff39301e8c1/Docker-images.png)

|Docker ps|
![image link](https://github.com/nikunjdaa-sit/Flask-MySQL-Docker-Compose/blob/78bfe09e92b95252108bb447bf133ff39301e8c1/Docker-ps.png)

|Dockerfile|
![image link](https://github.com/nikunjdaa-sit/Flask-MySQL-Docker-Compose/blob/78bfe09e92b95252108bb447bf133ff39301e8c1/Dockerfile.png)

|Flask Code|
![image link](https://github.com/nikunjdaa-sit/Flask-MySQL-Docker-Compose/blob/78bfe09e92b95252108bb447bf133ff39301e8c1/Flask-code.png)

|Application Output|
![image link](https://github.com/nikunjdaa-sit/Flask-MySQL-Docker-Compose/blob/78bfe09e92b95252108bb447bf133ff39301e8c1/Application-output.png)


# 🤝 Contributing

Contributions, improvements, and suggestions are welcome.

Feel free to fork the repository and create a pull request.

---

# 📜 License

This project is created for educational and learning purposes.

---

# 👨‍💻 Author

**Nikunj**

Cloud & DevOps Learner

GitHub: https://github.com/nikunjdaa-sit

LinkedIn: www.linkedin.com/in/nikunj-kumar-6a310b419

