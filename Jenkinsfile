pipeline {
    agent any

    stages {
        stage('Build & Tag Docker Image') {
            steps {
                script {
                    // Build and tag the Docker image with 'latest'
                    docker.build('sjagdale616/frontend:latest')
                }
            }
        }
        
        stage('Push Docker Image') {
            steps {
                script {
                    // Push the Docker image tagged with 'latest' to the registry
                    docker.withRegistry('https://registry.example.com', 'docker-cred') {
                        docker.image('sjagdale616/frontend:latest').push()
                    }
                }
            }
        }
    }
}
