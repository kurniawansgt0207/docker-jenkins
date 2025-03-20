pipeline {
    agent { label 'docker-agent' }
    stages {
        stage('Check Node') {
            steps {
                sh 'hostname'
                sh 'docker --version'
            }
        }
    }
}
