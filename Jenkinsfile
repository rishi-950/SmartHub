pipeline {
    agent any

    stages {
        stage('Checkout Code') {
            steps {
                git branch: 'master', url: 'https://github.com/rishi-950/SmartHub.git'
            }
        }

        stage('Build Docker Image') {
            steps {
                echo 'Building Docker image...'
                bat '"C:\\Program Files\\Docker\\Docker\\resources\\bin\\docker.exe" build -t smarthub-app .'
            }
        }

        stage('Run Docker Container') {
            steps {
                echo 'Running Docker container on port 9090...'
                // Stop existing container if running
                bat '"C:\\Program Files\\Docker\\Docker\\resources\\bin\\docker.exe" rm -f smarthub-container || exit 0'
                // Run new container
                bat '"C:\\Program Files\\Docker\\Docker\\resources\\bin\\docker.exe" run -d -p 9090:80 --name smarthub-container smarthub-app'
            }
        }
    }
}
