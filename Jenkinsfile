pipeline {
    agent any

    stages {
        stage('Checkout Code') {
            steps {
                echo 'Pulling latest code from GitHub...'
                git branch: 'main', url: 'https://github.com/raysharan619/My-app.git'
            }
        }

        stage('Test Build') {
            steps {
                echo 'Validating site files...'
                bat 'if exist index.html (echo "SUCCESS: index.html found.") else (exit 1)'
                bat 'if exist css\\style.css (echo "SUCCESS: style.css found.") else (exit 1)'
            }
        }

        stage('Deploy to IIS') {
            steps {
                echo 'Deploying application to Windows IIS...'
                bat 'xcopy /E /Y /I "%WORKSPACE%\\*" "C:\\inetpub\\wwwroot\\My-app"'
            }
        }
    }

    post {
        success {
            echo 'CI/CD Pipeline executed successfully! App deployed to IIS.'
        }
        failure {
            echo 'Pipeline failed. Check build logs for details.'
        }
    }
}