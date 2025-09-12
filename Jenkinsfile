pipeline {
    agent any
    environment {
        DOCKER_IMAGE = "python-app:latest"
    }
    stages {
        stage('Checkout Code') {
            steps {
                git branch: 'main', url: 'https://github.com/SathishitHubaccount/sample.git'
            }
        }
        stage('Build Docker Image') {
            steps {
                bat "docker build -t %DOCKER_IMAGE% ."
            }
        }
        stage('Run Docker Container') {
            steps {
                bat "docker ps -q --filter \"name=python-app\" | findstr . && docker stop python-app || echo Skipping"
                bat "docker rm python-app || echo No container to remove"
                bat "docker run -d -p 5000:5000 --name python-app %DOCKER_IMAGE%"
            }
        }
    }
}
