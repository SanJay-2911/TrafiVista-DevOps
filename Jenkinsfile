pipeline {
    agent any

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
