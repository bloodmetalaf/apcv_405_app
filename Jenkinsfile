pipeline {
    agent any

    environment {
        IMAGE_NAME = 'burdettbloodz/apcv_405_app'
    }

    stages {

        stage('Checkout') {
            steps {
                checkout scm
            }
        }

        stage('Run Tests') {
            steps {
                bat 'dotnet test apcv_405_app.sln'
            }
        }

        stage('Build Docker Image') {
            steps {
                bat 'docker build -t %IMAGE_NAME%:latest .'
                bat 'docker --version'
            }
        }

        stage('Push Docker Image') {
            steps {
                withCredentials([
                    usernamePassword(
                        credentialsId: 'dockerhub-credentials',
                        usernameVariable: 'DOCKER_USERNAME',
                        passwordVariable: 'DOCKER_PASSWORD'
                    )
                ]) {
                    bat 'docker login -u %DOCKER_USERNAME% -p %DOCKER_PASSWORD%'
                    bat 'docker push %IMAGE_NAME%:latest'
                }
            }
        }

        stage('Deploy Container') {
            steps {
                bat 'docker stop apcv_405_app >nul 2>&1'
                bat 'docker rm apcv_405_app >nul 2>&1'
                bat 'docker run -d --name apcv_405_app -p 9090:8080 %IMAGE_NAME%:latest'
            }
        }

        stage('Health Check') {
            steps {
                bat 'curl http://localhost:9090/health'
            }
        }
    }
}