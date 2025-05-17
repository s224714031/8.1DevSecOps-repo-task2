pipeline {
    agent any
    stages {
        stage('Checkout') {
            steps {
            git branch: 'main', url: ' https://github.com/s224714031/8.2CDevSecOps.git'
            }
        }
            stage('Install Dependencies') {
            steps {
            bat 'npm install'
            }
        }
            stage('Run Tests') {
            steps {
            bat 'npm test || exit /b 0' // Allows pipeline to continue despite test failures
            }
            
        }
            stage('Generate Coverage Report') {
            steps {
            // Ensure coverage report exists
            bat 'npm run coverage || exit /b 0'
            }
        }
            stage('NPM Audit (Security Scan)') {
            steps {
            bat 'npm audit || exit /b 0' // This will show known CVEs in the output
            }

            post {
                success {
                    emailext(
                        attachLog: true,
                        to: 'nadunhs25@gmail.com',
                        subject: "Build Success!",
                        body: "The build was successful and log is attached."
                    )
                }
            }

        }
    }
}
