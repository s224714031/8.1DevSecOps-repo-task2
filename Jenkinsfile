pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                git branch: 'main', url: 'https://github.com/s224714031/8.2CDevSecOps.git'
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
            post {
                success {
                    emailext(
                        attachLog: true,
                        to: 'nadunhs25@gmail.com',
                        subject: 'Run Tests Stage - SUCCESS',
                        body: 'The Run Tests stage completed successfully. Please find the attached log.'
                    )
                }
                failure {
                    emailext(
                        attachLog: true,
                        to: 'nadunhs25@gmail.com',
                        subject: 'Run Tests Stage - FAILURE',
                        body: 'The Run Tests stage failed. Please review the attached log for details.'
                    )
                }
            }
        }

        stage('Generate Coverage Report') {
            steps {
                bat 'npm run coverage || exit /b 0'
            }
        }

        stage('NPM Audit (Security Scan)') {
            steps {
                bat 'npm audit || exit /b 0'
            }
            post {
                success {
                    emailext(
                        attachLog: true,
                        to: 'nadunhs25@gmail.com',
                        subject: 'Security Scan Stage - SUCCESS',
                        body: 'The Security Scan stage completed successfully. Please find the attached log.'
                    )
                }
                failure {
                    emailext(
                        attachLog: true,
                        to: 'nadunhs25@gmail.com',
                        subject: 'Security Scan Stage - FAILURE',
                        body: 'The Security Scan stage failed. Please review the attached log for details.'
                    )
                }
            }
        }
    }
}
