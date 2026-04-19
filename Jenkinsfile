pipeline {
    agent any

    environment {
        DEPLOY_DIR = "E:\\xampp\\htdocs\\amsterdam"
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
                echo 'Deploying to XAMPP htdocs'

                bat '''
                if not exist "%DEPLOY_DIR%" mkdir "%DEPLOY_DIR%"
                
                REM Optional: clean old files
                del /Q "%DEPLOY_DIR%\\*"
                
                xcopy /E /I /Y "%WORKSPACE%\\*" "%DEPLOY_DIR%\\"
                '''
            }
        }
    }

    post {
        success {
            echo '✅ Deployment successful! Visit http://localhost/amsterdam'
        }
        failure {
            echo '❌ Build failed. Check logs.'
        }
    }
}
