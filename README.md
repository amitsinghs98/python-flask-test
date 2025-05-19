# Flask CI/CD Pipeline with Jenkins + Codeberg

## 🧾 Description
This project sets up a basic CI/CD pipeline using Jenkins, triggered by Codeberg webhooks to automatically deploy a simple Flask "Hello World" app to a server.

---

## 🚀 Tech Stack

- Python 3 + Flask
- Jenkins
- Codeberg (Git Repo)
- Webhooks
- (Optional: Docker)

---

## 🔧 Setup Instructions

### 1. Jenkins Setup

- Install Jenkins: `sudo apt install jenkins`
- Start Jenkins: `sudo systemctl start jenkins`
- Unlock Jenkins via browser
- Install recommended plugins + Git, Pipeline

### 2. Flask App Setup

- Clone repo: `git clone https://codeberg.org/<username>/<repo>.git`
- `cd repo`
- Install dependencies: `pip install -r requirements.txt`
- Run: `python app.py`

### 3. Webhook Setup 

- Go to Repo → Settings → Webhooks
- Add new webhook:
  - URL: `http://<jenkins-ip>:8080/generic-webhook-trigger/invoke?token=flask-deploy`
  - Trigger: On push

### 4. Jenkins Job

- New Pipeline Job
- Set Git repo as source
- Add token in webhook trigger config
- Add the pipeline stages to:
  - Clone code
  - Install dependencies
  - Restart app

---

## 📸 Screenshots 

---

## 🔍 How It Works

1. Developer pushes to Codeberg
2. Codeberg triggers a webhook
3. Jenkins receives webhook → pulls latest code
4. Jenkins installs dependencies and restarts the Flask app

---

## 📌 Assumptions & Limitations

- Server is assumed to have Python3 and pip installed.
- App restart is done via `nohup`; not production-ready.
- No reverse proxy (e.g., Nginx) or SSL included.
- Jenkins is publicly accessible to receive webhooks.
