pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }

        stage('Stop Old Containers') {
            steps {
                sh 'docker compose down || true'
            }
        }

        stage('Build and Start Containers') {
            steps {
                sh 'docker compose up --build -d'
            }
        }

        stage('Test API Health') {
            steps {
                sh '''
                sleep 10
                curl -f http://localhost:5000/health
                '''
            }
        }
    }
}
