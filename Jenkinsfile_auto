pipeline {
    agent any

    environment {
        IMAGE_NAME = "vue-consume-api"
        DOCKER_HUB_REPO = "sigitkurniawan0207/vue-consume-api"
    }

    stages {
        stage('Checkout') {
            steps {
                script {
                    git branch: 'main', credentialsId: 'ssh-key-github', url: 'https://github.com/kurniawansgt0207/vue-consume-api.git'
                }
            }
        }

        stage('Build Docker Image') {
            steps {
                script {
                    docker.build("${DOCKER_HUB_REPO}:latest")
                }
            }
        }

        stage('Login to Docker Hub') {
            steps {
                script {
                    withCredentials([usernamePassword(credentialsId: 'docker-hub-access', usernameVariable: 'DOCKER_USER', passwordVariable: 'DOCKER_PASS')]) {
                        sh "echo $DOCKER_PASS | docker login -u $DOCKER_USER --password-stdin"
                    }
                }
            }
        }

        stage('Push Image to Docker Hub') {
            steps {
                script {
                    docker.image("${DOCKER_HUB_REPO}:latest").push()
                }
            }
        }

        stage('Cleanup') {
            steps {
                sh "docker rmi ${DOCKER_HUB_REPO}:latest"
            }
        }
    }
}
