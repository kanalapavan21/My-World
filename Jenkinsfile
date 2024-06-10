pipeline {
    agent any // Indicates that the pipeline can run on any available agent (i.e., Jenkins slave)
 
    stages {
        stage('Checkout') {
            steps {
                // This step checks out the source code from your Git repository
                //git ''
                checkout scm
            }
        }
        stage('Build') {
            steps {
                // This step builds the Spring Boot application using Maven
                sh '/usr/share/maven/bin/mvn clean package -DskipTests'
            }
        }
         stage('Build Docker Image') {
            steps {
                // Build the Docker image
                script {
                    docker.build('hello-jenkins-image')
                }
            }
        }
        stage('Deploy') {
            steps {
                sh 'docker compose down'
                sh 'docker compose up -d'
            }
        }
    }
     post {
        success {
            // Actions to perform on successful build and deployment
            echo 'Build and deployment succeeded!'
        }
        failure {
            // Actions to perform on failed build or deployment
            echo 'Build or deployment failed.'
        }
    }
}