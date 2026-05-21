# Example Python Flask Crud

 Simple example python flask crud app for sqlite.
 
## Screenshots


![image](screenshots.png)  
 
 
### Installing (for linux)

open the terminal and follow the white rabbit.


```
git clone https://github.com/gurkanakdeniz/example-flask-crud.git
```
```
cd example-flask-crud/
```
```
python3 -m venv venv
```
```
source venv/bin/activate
```
```
pip install --upgrade pip
```
```
pip install -r requirements.txt
```
```
export FLASK_APP=crudapp.py
```
```
flask db init
```
```
flask db migrate -m "entries table"
```
```
flask db upgrade
```
```
flask run
```

## License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details
# 🚀 Flask CRUD DevOps CI/CD Project

This project is a Flask CRUD application deployed using a complete DevOps CI/CD pipeline with Jenkins, Docker, SonarQube, Kubernetes, and AWS EC2.

## 📌 Project Overview

The main goal of this project is to automate application build, test, code quality scan, Docker image creation, and deployment using DevOps tools.

## 🛠️ Technologies Used

- Python Flask
- Jenkins
- Docker
- Kubernetes
- SonarQube
- AWS EC2
- GitHub
- Linux (Ubuntu)

## 📂 Project Structure

- `app/` → Flask application files
- `Dockerfile` → Docker image configuration
- `Jenkinsfile` → Jenkins CI/CD pipeline
- `crudapp.py` → Main Flask application
- `requirements.txt` → Python dependencies

## ⚙️ CI/CD Pipeline Flow

1. Developer pushes code to GitHub
2. Jenkins pulls the source code
3. Jenkins installs dependencies
4. SonarQube performs code quality scan
5. Docker image is built
6. Docker container is deployed
7. Application runs on AWS EC2

## ✅ Features

- Automated CI/CD pipeline
- Docker containerization
- Jenkins automation
- SonarQube integration
- Flask CRUD operations
- AWS deployment
- Beginner-friendly DevOps project

## ▶️ How to Run Project

### Clone Repository

```bash
git clone https://github.com/mahi8867/flask-curd.git
