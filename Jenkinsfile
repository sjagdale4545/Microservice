pipeline {
    agent any

    stages {
        stage('Build & Tag Docker Image') {
            steps {
                script {
                    // Generate a timestamp-based tag for uniqueness
                    def dockerTag = "latest-${env.BUILD_NUMBER}-${env.BUILD_ID}".toLowerCase()

                    // Build Docker image with the latest tag
                    withDockerRegistry(credentialsId: 'docker-cred', toolName: 'docker') {
                        sh "docker build -t sjagdale616/frontend:latest -t sjagdale616/frontend:${dockerTag} ."
                    }
                    
                    // Output the generated tag for reference
                    echo "Docker Tag: ${dockerTag}"
                }
            }
        }
        
        stage('Push Docker Image') {
            steps {
                script {
                    // Push the Docker image with the latest tag
                    withDockerRegistry(credentialsId: 'docker-cred', toolName: 'docker') {
                        sh "docker push sjagdale616/frontend:latest"
                        sh "docker push sjagdale616/frontend:${dockerTag}"
                    }
                }
            }
        }
    }
}
