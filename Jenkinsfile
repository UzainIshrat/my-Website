pipeline {
    agent any
    environment {
        APP_IP = '172.31.2.249'
    }
    stages {
        stage('Checkout') {
            steps { checkout scm }
        }
        stage('Deploy') {
            steps {
                sshagent(['app-server-key']) {
                    sh """
                    scp -o StrictHostKeyChecking=no index.html ubuntu@${APP_IP}:/var/www/html/
                    ssh -o StrictHostKeyChecking=no ubuntu@${APP_IP} 'sudo systemctl reload nginx'
                    """
                }
            }
        }
    }
}
