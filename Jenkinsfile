pipeline {
    agent any

    stages { 
        stage('Remove Existing Docker Image') {
            steps {
                script {
                    // Use Docker CLI tool to remove existing frontend image if it exists
                    sh "docker rmi -f sjagdale616/frontend || true"
                }
            }
        }
        stage('Build & Tag Docker Image') {
            steps {
                script {
                    withDockerRegistry(credentialsId: 'docker-cred', toolName: 'docker') {
                        sh "docker build -t sjagdale616/frontend ."
                    }
                }
            }
        }
        
        stage('Push Docker Image') {
            steps {
                script {
                    withDockerRegistry(credentialsId: 'docker-cred', toolName: 'docker') {
                        sh "docker push sjagdale616/frontend"
                    }
                }
            }
        }
    }
}
