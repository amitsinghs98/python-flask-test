# Python Flask Hello World CI/CD with Jenkins

This project demonstrates how to deploy a simple Python Flask "Hello World" application to a cloud VM using Jenkins and GitHub. Jenkins is used for automating the deployment pipeline.

---

## 🧰 Tech Stack

- Python 3.x
- Flask
- Jenkins
- GitHub
- Ubuntu (Cloud VM or Local)

---

## 📂 Project Structure

python-flask-test/
├── app.py
├── requirements.txt
└── ...


---

## 🚀 Jenkins CI/CD Pipeline Workflow

This pipeline performs the following:

1. **Clone the GitHub Repo**
2. **Create & Activate Python Virtual Environment**
3. **Install Dependencies**
4. **Start the Flask App**
5. **Restart the App on New Push**

---

## 🔧 Jenkins Setup

### 1. Install Jenkins

Install Jenkins and required dependencies (Java 17 or lower is recommended, not Java 21).

```bash
sudo apt update
sudo apt install openjdk-17-jdk
```
---

## 2. Install Python and pip
sudo apt install python3 python3-pip python3-venv

---

## 3. Create a Jenkins Pipeline Job
Jenkinsfile Example

pipeline {
    agent any

    environment {
        VENV_PATH = "${WORKSPACE}/venv"
    }

    stages {
        stage('Clone Repo') {
            steps {
                git credentialsId: 'your-git-creds-id', url: 'https://github.com/amitsinghs98/python-flask-test'
            }
        }

        stage('Setup Python Environment') {
            steps {
                sh '''
                    python3 -m venv ${VENV_PATH}
                    ${VENV_PATH}/bin/pip install --upgrade pip
                    ${VENV_PATH}/bin/pip install -r requirements.txt
                '''
            }
        }

        stage('Restart App') {
            steps {
                sh '''
                    pkill -f app.py || true
                    nohup ${VENV_PATH}/bin/python app.py &
                '''
            }
        }
    }
}

---

## Configure GitHub Webhook
Go to your GitHub repo → Settings → Webhooks

Add a new webhook:

Payload URL: http://<your-server-ip>:8080/github-webhook/

Content type: application/json

Trigger: Just the push event

In Jenkins, under your job → Configure:

---

## Check "GitHub hook trigger for GITScm polling"

---

## 🐍 Sample Output
Visit: http://<your-server-ip>:5000

Response:
Hello, World!



