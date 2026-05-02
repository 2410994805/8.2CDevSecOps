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

        stage('SonarCloud Analysis') {
            steps {
                withCredentials([string(credentialsId: 'SONAR_TOKEN', variable: 'SONAR_TOKEN')]) {
                    bat '''
                    if not exist sonar-scanner (
                        powershell -Command "Invoke-WebRequest -Uri https://binaries.sonarsource.com/Distribution/sonar-scanner-cli/sonar-scanner-6.2.1.4610-windows-x64.zip -OutFile sonar-scanner.zip"
                        powershell -Command "Expand-Archive -Path sonar-scanner.zip -DestinationPath . -Force"
                        ren sonar-scanner-6.2.1.4610-windows-x64 sonar-scanner
                    )
                    sonar-scanner\\bin\\sonar-scanner.bat -Dsonar.login=%SONAR_TOKEN%
                    '''
                }
            }
        }
    }
}