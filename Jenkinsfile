pipeline {
    agent any

    environment {
        DEPLOY_DIR = "E:\\deploy\\my-website"
    }

    stages {

        stage('Checkout') {
            steps {
                echo 'Code is automatically checked out by Jenkins (Multibranch)'
            }
        }

        stage('Build') {
            steps {
                echo 'No build required for static HTML project'
            }
        }

        stage('Test') {
            steps {
                echo 'Checking if index.html exists'

                bat '''
                if exist "%WORKSPACE%\\index.html" (
                    echo File exists
                ) else (
                    echo index.html not found
                    exit 1
                )
                '''
            }
        }

        stage('Deploy') {
            steps {
                echo 'Deploying to local folder'

                bat '''
                if not exist "%DEPLOY_DIR%" mkdir "%DEPLOY_DIR%"
                xcopy /E /I /Y "%WORKSPACE%\\*" "%DEPLOY_DIR%\\"
                '''
            }
        }
    }

    post {
        success {
            echo '✅ Deployment successful!'
        }
        failure {
            echo '❌ Build failed. Check logs.'
        }
    }
}
