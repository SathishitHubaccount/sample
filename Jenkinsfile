pipeline {
    agent any

    environment {
        DOCKER_IMAGE = "python-app:latest"
    }

    stages {
        stage('Checkout Code') {
            steps {
                git branch: 'main', url: 'https://github.com/SathishitHubaccount/sample'
            }
        }

        stage('Build Docker Image') {
            steps {
                script {
                    sh "docker build -t ${DOCKER_IMAGE} ."
                }
            }
        }

        stage('Run Docker Container') {
            steps {
                script {
                    // Stop old container if running
                    sh "docker ps -q --filter 'name=python-app' | grep -q . && docker stop python-app || true"
                    sh "docker rm python-app || true"

                    // Run new container
                    sh "docker run -d -p 5000:5000 --name python-app ${DOCKER_IMAGE}"
                }
            }
        }
    }

    post {
        success {
            echo "🚀 Python app deployed successfully in Docker!"
        }
        failure {
            echo "❌ Deployment failed!"
        }
    }
}
