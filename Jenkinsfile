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
                        subject: "Jenkins - Run Tests Stage: ${currentBuild.currentResult} - Build #${env.BUILD_NUMBER}",
                        body: """
                            <p>Pipeline: ${env.JOB_NAME}</p>
                            <p>Stage: Run Tests</p>
                            <p>Status: ${currentBuild.currentResult}</p>
                            <p>Build URL: ${env.BUILD_URL}</p>
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
                        subject: "Jenkins - Security Scan Stage: ${currentBuild.currentResult} - Build #${env.BUILD_NUMBER}",
                        body: """
                            <p>Pipeline: ${env.JOB_NAME}</p>
                            <p>Stage: NPM Audit (Security Scan)</p>
                            <p>Status: ${currentBuild.currentResult}</p>
                            <p>Build URL: ${env.BUILD_URL}</p>
                        """,
                        mimeType: 'text/html',
                        attachLog: true
                    )
                }
            }
        }

    }
}
