pipeline {
    agent any
    environment {
        APP_IP = '13.201.132.110'
    }
    stages {
        stage('Checkout') {
            steps { checkout scm }
        }
        stage('Deploy') {
    steps {
        sshagent(['app-server-key']) {
            sh '''
            tar --exclude=.git --exclude=Jenkinsfile --exclude=README.md -czf - . | \
            ssh -o StrictHostKeyChecking=no ubuntu@${APP_IP} "tar -xzf - -C /var/www/html"
            '''
        }
    }
}
