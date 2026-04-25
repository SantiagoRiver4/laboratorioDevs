pipeline {
    agent any

    stages {

        stage('Prepare') {
            steps {
                echo 'Preparando entorno...'
            }
        }

        stage('Install Dependencies') {
            steps {
                bat 'py -m pip install -r requirements.txt'
            }
        }

        stage('Run Tests') {
            steps {
                bat 'py -m pytest'
            }
        }

        stage('Security Scan') {
            steps {
                bat 'py -m bandit -r . || exit 0'
            }
        }

        stage('Build Docker Image') {
            steps {
                bat 'docker build -t devsecops-app .'
            }
        }

        stage('Deploy Container') {
            steps {
                bat 'docker run -d -p 5000:5000 devsecops-app'
            }
        }
    }
}