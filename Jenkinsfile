pipeline {
    agent any

    stages {
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
        success {
            emailext (
                to: "drushmitha2004@gmail.com",
                subject: "SUCCESS: Build ${env.BUILD_NUMBER}",
                body: "Build passed successfully!"
            )
        }

        failure {
            emailext (
                to: "drushmitha2004@gmail.com",
                subject: "FAILED: Build ${env.BUILD_NUMBER}",
                body: "Build failed. Check Jenkins console."
            )
        }
    }
}

post {
    success {
        emailext (
            subject: "Jenkins Build Notification",
            body: "Build completed successfully. Please check Jenkins for details.",
            to: "drushmitha2004@gmail.com"
        )
    }
}
