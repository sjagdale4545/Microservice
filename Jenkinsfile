pipeline {
    agent any

    environment {
        // Define Docker registry and image details
        //withDockerRegistry(credentialsId: 'docker-cred', toolName: 'docker')
        //DOCKER_REGISTRY = 'your-docker-registry'
        IMAGE_NAME = 'sjagdale616/frontend'
    }

    stages {
        stage('Build') {
            steps {
                script {
                    // Get a unique tag using the Jenkins build number
                    {
                    withDockerRegistry(credentialsId: 'docker-cred', toolName: 'docker')
                    
                    IMAGE_TAG = "${env.BUILD_NUMBER}"
                    // Build and push the Docker image
                        {
                            sh """
                        docker build -t ${DOCKER_REGISTRY}/${IMAGE_NAME}:${IMAGE_TAG} .
                        docker push ${DOCKER_REGISTRY}/${IMAGE_NAME}:${IMAGE_TAG}
                    """
                }
            }
            }
        }
    }

        stage('Deploy') {
            steps {
                script {
                    // Update the Kubernetes deployment with the new image tag
                    sh """
                        kubectl set image deployment/frontend server=${DOCKER_REGISTRY}/${IMAGE_NAME}:${IMAGE_TAG} --record
                    """
                }
            }
        }
    }
}
