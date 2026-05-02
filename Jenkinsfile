pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                git branch: 'main', url: 'https://github.com/2410994805/8.2CDevSecOps.git'
            }
        }

        stage('Install Dependencies') {
            steps {
                bat 'call npm install'
            }
        }

        stage('Run Tests') {
            steps {
                bat 'call npm test || exit /b 0'
            }
        }

        stage('Generate Coverage Report') {
            steps {
                bat 'call npm run coverage || exit /b 0'
            }
        }

        stage('NPM Audit (Security Scan)') {
            steps {
                bat 'call npm audit || exit /b 0'
            }
        }
    }
}
