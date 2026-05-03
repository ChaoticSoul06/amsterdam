pipeline {
    agent any

    environment {
        IMAGE_NAME = "amsterdam"
        CONTAINER_NAME = "amsterdam_${env.BRANCH_NAME}"
        PORT = "808${env.BUILD_NUMBER}"
    }

    stages {

        stage('Build Docker Image') {
            steps {
                echo "Building Docker image..."
                bat 'docker build -t %IMAGE_NAME% .'
            }
        }

        stage('Remove Old Container') {
            steps {
                echo "Removing old container if exists..."
                bat '''
                docker rm -f %CONTAINER_NAME% || exit 0
                '''
            }
        }

        stage('Run Container') {
            steps {
                echo "Running container..."
                bat '''
                docker run -d -p %PORT%:80 --name %CONTAINER_NAME% %IMAGE_NAME%
                '''
            }
        }
    }

    post {
        success {
            echo "Deployed at http://localhost:${env.PORT}"
        }
    }
}