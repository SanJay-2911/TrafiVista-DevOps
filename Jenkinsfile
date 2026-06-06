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
        stage('Backup Current Images') {
            steps {
                sh '''
                    docker tag trafivista-cicd-backend:latest trafivista-cicd-backend:rollback || true
                    docker tag trafivista-cicd-frontend:latest trafivista-cicd-frontend:rollback || true
                '''
            }
        }
        stage('Docker Compose Build') {
            steps {
                sh 'docker-compose down'
                sh 'docker-compose up -d --build'
            }
        }
    }
    post {
        failure {
            echo 'Build failed! Rolling back to previous version...'
            sh '''
                docker-compose down || true
                docker tag trafivista-cicd-backend:rollback trafivista-cicd-backend:latest || true
                docker tag trafivista-cicd-frontend:rollback trafivista-cicd-frontend:latest || true
                docker-compose up -d || true
            '''
        }
        success {
            echo 'Deployment successful!'
        }
    }
}
