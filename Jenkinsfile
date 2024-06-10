pipeline {
    agent any
    environment {
        DOCKER_IMAGE = 'hello-jenkins'
        COMPOSE_FILE = 'docker-compose.yaml'
    }
    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }
        stage('Build Docker Image') {
            steps {
                script {
                    docker.build("${DOCKER_IMAGE}:${env.BUILD_ID}")
                }
            }
        }
        stage('Deploy') {
            steps {
                script {
                    // Stop existing containers
                    sh "docker compose down"
                    
                    // Deploy new containers
                    sh "docker compose up"
                }
            }
        }
    }
    post {
        always {
            cleanWs()
        }
    }
}
