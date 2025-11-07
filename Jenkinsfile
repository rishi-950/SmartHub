pipeline {
    agent any

    environment {
        IMAGE_NAME = "smarthub-app"
        CONTAINER_NAME = "smarthub-container"
        PORT = "9090"
        DOCKER = '"C:\\Program Files\\Docker\\Docker\\resources\\bin\\docker.exe"'
    }

    stages {

        stage('Checkout Code') {
            steps {
                echo 'Checking out code from GitHub...'
                git branch: 'master', url: 'https://github.com/rishi-950/SmartHub.git'
            }
        }

        stage('Build Docker Image') {
            steps {
                echo 'Building Docker image...'
                bat "${DOCKER} build -t ${IMAGE_NAME} ."
            }
        }

        stage('Stop Old Container') {
            steps {
                echo 'Stopping old container if it exists...'
                bat "${DOCKER} stop ${CONTAINER_NAME} 2>nul || exit 0"
                bat "${DOCKER} rm ${CONTAINER_NAME} 2>nul || exit 0"
            }
        }

        stage('Run Docker Container') {
            steps {
                echo "Running new Docker container on port ${PORT}..."
                bat "${DOCKER} run -d -p ${PORT}:80 --name ${CONTAINER_NAME} ${IMAGE_NAME}"
            }
        }
    }

    post {
        success {
            echo "SmartHub deployed successfully! Open http://localhost:${PORT}"
        }
        failure {
            echo "Pipeline failed. Check logs for errors."
        }
    }
}
