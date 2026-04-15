pipeline {
    agent any
    stages {
        stage('Checkout') {
            steps { git branch: 'main', url: 'https://github.com/Sushmaganda/Devops_Pipeline.git' }
        }
        stage('Build Docker Image') {
            steps { sh "docker build -t flask-app:${BUILD_NUMBER} ." }
        }
        stage('Run Unit Tests') {
            steps { sh "docker run --rm flask-app:${BUILD_NUMBER} pytest -v" }
        }
        stage('Deploy with Docker Compose') {
            steps {
                sh "docker-compose down"
                sh "docker-compose up -d --build"
            }
        }
    }
    post {
        success { echo "Deployment successful!" }
        failure { echo "Pipeline failed. Check logs." }
    }
}
