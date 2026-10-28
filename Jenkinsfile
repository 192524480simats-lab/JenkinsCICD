
pipeline {
    agent any

    triggers {
        pollSCM('H/2 * * * *')
    }

    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }

        stage('Install Dependencies') {
            steps {
                bat 'python -m pip install -r requirements.txt'
            }
        }

        stage('Run Tests') {
            steps {
                bat 'python -m pytest -q'
            }
        }

        stage('Build Docker Image') {
            steps {
                bat 'docker build -t ci-cd-sample:latest .'
            }
        }

        stage('Deploy Application') {
            steps {
                bat 'docker rm -f ci-cd-sample 2>NUL & docker run -d --name ci-cd-sample -p 5001:5000 ci-cd-sample:latest'
            }
        }
    }
}
