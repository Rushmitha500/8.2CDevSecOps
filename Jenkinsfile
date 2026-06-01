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
    always {
        emailext (
            to: "drushmitha2004@gmail.com",
            subject: "Build ${currentBuild.currentResult}: ${env.BUILD_NUMBER}",
            body: "Pipeline completed with status: ${currentBuild.currentResult}"
        )
    }
}
}
