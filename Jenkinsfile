pipeline {
    agent any

    stages {
        stage('Pull Latest Docker Image') {
            steps {
                script {
                    // Step to pull the latest Docker image
                    sh "docker pull sjagdale616/frontend:latest"
                }
            }
        }

        stage('Build & Tag Docker Image') {
            steps {
                script {
                    // Step to build and tag Docker image
                    withDockerRegistry(credentialsId: 'docker-cred', toolName: 'docker') {
                        sh "docker build -t sjagdale616/frontend:latest ."
                    }
                }
            }
        }
        
        stage('Push Docker Image') {
            steps {
                script {
                    // Step to push Docker image
                    withDockerRegistry(credentialsId: 'docker-cred', toolName: 'docker') {
                        sh "docker push sjagdale616/frontend:latest"
                    }
                }
            }
        }
    }
}
