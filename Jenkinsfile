pipeline {
    agent any

    stages {
        stage('Check Docker Access') {
            steps {
                sh 'docker ps'
            }
        }

        stage('Checkout') {
            steps {
                git branch: 'main', url: 'https://github.com/Abhinav-AI-dev/flask-starter.git'
            }
        }

        stage('Build Docker Image') {
            steps {
                sh 'docker build -t flask-student .'
            }
        }

        stage('Stop Previous Container') {
            steps {
                sh '''
                docker stop flask-container || true
                docker rm flask-container || true
                '''
            }
        }

        stage('Run New Container') {
            steps {
                sh 'docker run -d --name flask-container -p 5000:5000 flask-student'
            }
        }
    }

    post {
        success {
            echo 'Deployment successful!'
        }
        failure {
            echo 'Deployment failed!'
        }
    }
}
