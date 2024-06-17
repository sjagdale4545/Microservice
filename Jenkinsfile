pipeline {
    agent any

    stages {
        stage('Build & Tag Docker Image') {
            steps {
                script {
                    // Generate a timestamp-based tag for the Docker image
                    def dockerTag = "sjagdale616/frontend:latest-${env.BUILD_NUMBER}"
                    
                    // Build and tag the Docker image
                    withDockerRegistry(credentialsId: 'docker-cred', toolName: 'docker') {
                        sh "docker build -t ${dockerTag} ."
                        sh "docker tag ${dockerTag} sjagdale616/frontend:latest"
                    }
                }
            }
        }
        
        stage('Push Docker Image') {
            steps {
                script {
                    // Push the Docker image with latest tag to the registry
                    withDockerRegistry(credentialsId: 'docker-cred', toolName: 'docker') {
                        sh "docker push sjagdale616/frontend:latest"
                    }
                }
            }
        }
    }
}
