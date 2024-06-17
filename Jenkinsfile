pipeline {
    agent any

    environment {
        IMAGE_NAME = 'sjagdale616/frontend'
        IMAGE_TAG = 'latest'
    }

    stages {
        stage('Build & Tag Docker Image') {
            steps {
                script {
                    // Build the Docker image
                    def dockerfilePath = './Dockerfile' // Adjust if the Dockerfile is located elsewhere
                    sh "docker build -t ${IMAGE_NAME}:${IMAGE_TAG} -f ${dockerfilePath} ."
                }
            }
        }
        
        stage('Push Docker Image') {
            steps {
                script {
                    // Push the Docker image to the registry
                    withDockerRegistry(credentialsId: 'docker-cred', url: 'https://index.docker.io/v1/') {
                        sh "docker push ${IMAGE_NAME}:${IMAGE_TAG}"
                    }
                }
            }
        }
    }
    
    post {
        always {
            script {
                // Clean up Docker images after the pipeline runs
                sh "docker rmi ${IMAGE_NAME}:${IMAGE_TAG} || true"
            }
        }
        success {
            echo 'Docker image build and push succeeded!'
        }
        failure {
            echo 'Docker image build and push failed.'
        }
    }
}
