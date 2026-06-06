pipeline {
    agent any
    environment {
        BACKEND_PORT = '8000'
        FRONTEND_PORT = '3000'
    }
    stages {
        stage('Clone Repository') {
            steps {
                git branch: 'main',
                url: 'https://github.com/SanJay-2911/TrafiVista-DevOps.git'
            }
        }
        stage('Docker Compose Build') {
            steps {
                sh 'docker-compose down'
                sh 'docker-compose up -d --build'
            }
        }
    }
}
