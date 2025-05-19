pipeline {
    agent any

    environment {
        APP_DIR = '/opt/flask-app'
    }

    stages {
        stage('Clone Repo') {
            steps {
               git branch: 'main', credentialsId: 'github', url: 'https://github.com/amitsinghs98/python-flask-test'
            }
        }

        stage('Install Dependencies') {
            steps {
                 sh '''
                  python3 -m venv venv
            . venv/bin/activate
            pip install --upgrade pip
            pip install -r requirements.txt
                '''
            }
        }

        stage('Restart App') {
            steps {
                sh """
                  pkill -f app.py || true
            cd $WORKSPACE
            nohup python3 app.py &
                """
            }
        }
    }
}
