pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }

        stage('Build') {
            steps {
                echo 'Building application...'
            }
        }

        stage('Test') {
            steps {
                echo 'Running tests...'
            }
        }
    }

    post {
        always {
            emailext (
                to: "drushmitha2004@gmail.com",
                subject: "Jenkins Build ${currentBuild.currentResult} - #${env.BUILD_NUMBER}",
                body: """
Build Status: ${currentBuild.currentResult}
Build Number: ${env.BUILD_NUMBER}

Check Jenkins for full details: ${env.BUILD_URL}
"""
            )
        }
    }
}
