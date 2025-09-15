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
        stage('Check Docker') {
            steps {
                bat 'docker --version'
            }
        }

        stage('Build Docker Image') {
            steps {
                bat "docker build -t %DOCKER_IMAGE% ."
            }
        }
        stage('Run Docker Container') {
            steps {
               powershell '''
                        $container = docker ps -q --filter "name=python-app"
                        if ($container) { docker stop $container } else { echo "Skipping" }
                        '''

            }
        }
    }
}
