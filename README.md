🚀 Cloud File Storage App
A Cloud-Based File Upload System using AWS EC2, S3, DynamoDB & Flask
<p align="center"> <img src="https://img.shields.io/badge/AWS-EC2%20%7C%20S3%20%7C%20DynamoDB-orange?logo=amazon-aws&logoColor=white" /> <img src="https://img.shields.io/badge/Python-Flask-blue?logo=python&logoColor=white" /> <img src="https://img.shields.io/badge/Frontend-HTML-lightgrey?logo=html5&logoColor=white" /> <img src="https://img.shields.io/badge/Server-Gunicorn-brightgreen" /> </p>
📌 Project Overview

This project is a Cloud File Storage System created using:

Amazon EC2 – for hosting backend & frontend

Amazon S3 – for file storage

DynamoDB – for metadata logging

Flask (Python) – backend REST API

Gunicorn – production WSGI server

The user uploads a file → it gets stored in S3 → and metadata is saved in DynamoDB.

🏗️ Architecture Diagram

User
│
│ (Upload File)
▼
Frontend (HTML + Port 8000)
│
│ (POST request)
▼
Flask Backend (Port 5000)
│
├── Upload file to S3
│
└── Save metadata to DynamoDB


🔧 AWS Resources Used
Component	Value
S3 Bucket	demo-s3-drive123
DynamoDB Table	demo-s3-drive123
Region	ap-south-1
EC2 Server (Old)	15.206.203.95
JWT Secret	MyCloudAppSecret2025
Frontend Port	8000
Backend Port	5000
OS	Amazon Linux 2
Gunicorn	✔ Enabled
🌐 Demo Screenshot

(Add a folder named screenshots/ and include images.)

📁 Project Structure

cloud-file-storage-app/
│── app.py
│── upload.html
│── requirements.txt
│── README.md
│── screenshots/

⚙️ 1. EC2 Setup Commands
🔹 Connect to EC2
ssh -i "ashwini-key.pem" ec2-user@15.206.203.95

🔹 Update system
sudo yum update -y

