pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                git branch: 'main',
                url: 'https://github.com/oscar2960/CI-CD'
            }
        }

        stage('Build Docker Images') {
            steps {
                bat 'docker-compose build'
            }
        }

        stage('Run Containers') {
            steps {
                bat '''
                docker-compose down --remove-orphans
                docker rm -f db-container || true
                docker rm -f app-container || true
                docker-compose up -d
                '''
            }
        }
    }
}
