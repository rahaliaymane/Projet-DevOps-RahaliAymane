pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                echo 'Checkout repository'
            }
        }

        stage('Build') {
            steps {
                echo 'Build step'
            }
        }

        stage('Test') {
            steps {
                echo 'Test step'
            }
        }
    }
}
post {
    success {
        script {
            try {
                slackSend(
                    channel: '#jenkins',
                    credentialId: 'slack-webhook',
                    message: "✅ Build SUCCESS : ${env.JOB_NAME} #${env.BUILD_NUMBER}"
                )
            } catch (e) {
                echo "Slack notification skipped (configuration issue)"
            }
        }
    }
    failure {
        script {
            try {
                slackSend(
                    channel: '#jenkins',
                    credentialId: 'slack-webhook',
                    message: "❌ Build FAILED : ${env.JOB_NAME} #${env.BUILD_NUMBER}"
                )
            } catch (e) {
                echo "Slack notification skipped (configuration issue)"
            }
        }
    }
}
