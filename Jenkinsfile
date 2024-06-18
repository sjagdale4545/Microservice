pipeline {
    agent any

    stages {
        stage('Delete Docker Image from Docker Hub') {
            steps {
                script {
                    // Remove the existing Docker image from Docker Hub
                    docker.withRegistry('https://registry.hub.docker.com', 'docker-cred') {
                        sh "docker rmi sjagdale616/frontend:latest"
                    }
                }
            }
        }

        stage('Build & Tag Docker Image') {
            steps {
                script {
                    // Build the Docker image
                    docker.build('sjagdale616/frontend:latest', '.')
                }
            }
        }
        
        stage('Push Docker Image') {
            steps {
                script {
                    // Push the Docker image to Docker Hub
                    docker.withRegistry('https://registry.hub.docker.com', 'docker-cred') {
                        sh "docker push sjagdale616/frontend:latest"
                    }
                }
            }
        }
    }
}
