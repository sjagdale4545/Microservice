pipeline {
    agent any

    stages {
        stage('Pull Latest Docker Image') {
            steps {
                script {
                    // Pulling the latest image from Docker Hub
                    sh "docker pull sjagdale616/frontend:latest"
                }
            }
        }

        stage('Build & Tag Docker Image') {
            steps {
                script {
                    // Using Docker registry credentials 'docker-cred' and Docker tool
                    withDockerRegistry(credentialsId: 'docker-cred', toolName: 'docker') {
                        // Building the Docker image with tag sjagdale616/frontend:latest
                        sh "docker build -t sjagdale616/frontend:latest ."
                    }
                }
            }
        }
        
        stage('Push Docker Image') {
            steps {
                script {
                    // Using Docker registry credentials 'docker-cred' and Docker tool
                    withDockerRegistry(credentialsId: 'docker-cred', toolName: 'docker') {
                        // Pushing the Docker image to the registry
                        sh "docker push sjagdale616/frontend:latest"
                    }
                }
            }
        }
    }
}
