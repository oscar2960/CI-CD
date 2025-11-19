pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                git branch: 'main',
                url: 'YOUR_GITHUB_REPO_URL'
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
