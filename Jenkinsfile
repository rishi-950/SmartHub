pipeline {
    agent any

    stages {
        stage('Checkout Code') {
            steps {
                git 'https://github.com/rishi-950/SmartHub.git'
            }
        }

        stage('Build Docker Image') {
            steps {
                script {
                    echo "Building Docker image..."
                    sh 'docker build -t my-website .'
                }
            }
        }

        stage('Run Docker Container') {
            steps {
                script {
                    echo "Stopping old container if running..."
                    sh 'docker stop my-website-container || true'
                    sh 'docker rm my-website-container || true'

                    echo "Running new container on port 9090..."
                    sh 'docker run -d -p 9090:80 --name my-website-container my-website'
                }
            }
        }
    }
}
