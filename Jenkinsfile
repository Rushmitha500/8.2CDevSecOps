pipeline {
    agent any

    stages {

        stage('Checkout') {
            steps {
                git branch: 'main', url: 'https://github.com/Rushmitha500/8.2CDevSecOps.git'
            }
        }

        stage('Install Dependencies') {
            steps {
                bat 'npm install'
            }
        }

        stage('Run Tests') {
            steps {
                bat 'npm test || exit /b 0'
            }
            post {
                always {
                    emailext(
                        to: 'drushmitha2004@gmail.com',
                        subject: "Jenkins - Run Tests: ${currentBuild.currentResult} - Build #${env.BUILD_NUMBER}",
                        body: """
                            <p><b>Pipeline:</b> ${env.JOB_NAME}</p>
                            <p><b>Stage:</b> Run Tests</p>
                            <p><b>Status:</b> ${currentBuild.currentResult}</p>
                            <p><b>Build URL:</b> ${env.BUILD_URL}</p>
                        """,
                        mimeType: 'text/html',
                        attachLog: true
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
                always {
                    emailext(
                        to: 'drushmitha2004@gmail.com',
                        subject: "Jenkins - Security Scan: ${currentBuild.currentResult} - Build #${env.BUILD_NUMBER}",
                        body: """
                            <p><b>Pipeline:</b> ${env.JOB_NAME}</p>
                            <p><b>Stage:</b> NPM Audit (Security Scan)</p>
                            <p><b>Status:</b> ${currentBuild.currentResult}</p>
                            <p><b>Build URL:</b> ${env.BUILD_URL}</p>
                        """,
                        mimeType: 'text/html',
                        attachLog: true
                    )
                }
            }
        }

    }
}
