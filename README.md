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

🔹 Install python & git
sudo yum install git python3 -y

⚙️ 2. Install Backend Dependencies
pip3 install flask boto3 gunicorn

🐍 3. Backend API – app.py
from flask import Flask, request, jsonify
import boto3, datetime
from werkzeug.utils import secure_filename

app = Flask(__name__)

S3_BUCKET = "demo-s3-drive123"
DYNAMO_TABLE = "demo-s3-drive123"
REGION = "ap-south-1"
JWT_SECRET = "MyCloudAppSecret2025"

s3 = boto3.client("s3", region_name=REGION)
dynamodb = boto3.resource("dynamodb", region_name=REGION)
table = dynamodb.Table(DYNAMO_TABLE)

@app.route("/upload", methods=["POST"])
def upload_file():
    file = request.files["file"]
    filename = secure_filename(file.filename)
    s3.upload_fileobj(file, S3_BUCKET, filename)

    table.put_item(Item={
        "filename": filename,
        "uploaded_at": str(datetime.datetime.utcnow()),
    })

    return jsonify({"message": "File uploaded successfully!", "file": filename})

@app.route("/")
def home():
    return "Backend is Running!"

if __name__ == "__main__":
    app.run(host="0.0.0.0", port=5000)

🌐 4. Frontend UI – upload.html
<!DOCTYPE html>
<html>
<head>
<title>Cloud File Upload</title>
</head>
<body>
<h2>Upload File to Cloud Storage</h2>
<form action="http://15.206.203.95:5000/upload" method="POST" enctype="multipart/form-data">
    <input type="file" name="file" required>
    <button type="submit">Upload</button>
</form>
</body>
</html>

🧪 5. Test Frontend Locally
python3 -m http.server 8000


Open:

http://15.206.203.95:8000/upload.html

🚀 6. Start Backend (Development Mode)
python3 app.py

🚀 7. Start Backend (Production Mode - Gunicorn)
gunicorn --bind 0.0.0.0:5000 app:app --daemon

✔ Check if running
curl http://localhost:5000

🌍 8. (Optional) Nginx Setup
sudo amazon-linux-extras install nginx1 -y
sudo systemctl start nginx

🔑 9. IAM Permissions Required

AmazonS3FullAccess

AmazonDynamoDBFullAccess

💻 10. Full Command List (Used in Project)
sudo yum update -y
sudo yum install git python3 -y
pip3 install flask boto3 gunicorn
python3 -m http.server 8000
python3 app.py
gunicorn --bind 0.0.0.0:5000 app:app --daemon
ssh -i "ashwini-key.pem" ec2-user@15.206.203.95

📝 11. How It Works

✔ User uploads file
✔ Flask receives file
✔ Uploads to S3
✔ Saves metadata to DynamoDB
✔ Returns success message

⭐ 12. Future Improvements

Add login/auth (JWT)

Add file preview

Add delete option

Add downloadable link from S3

❤️ 13. Author

Ashwini G Rathod
Cloud Engineer
aws/azure
