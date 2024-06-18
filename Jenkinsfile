pipeline {
    agent any

    environment {
        DOCKER_IMAGE = 'sjagdale616/frontend'
        DOCKER_TAG = 'latest'
        DOCKER_CREDENTIALS_ID = 'docker-cred'
        DOCKER_TOOL = 'docker'
    }

    stages {
        stage('Build Docker Image') {
            steps {
                script {
                    withDockerRegistry(credentialsId: DOCKER_CREDENTIALS_ID, toolName: DOCKER_TOOL) {
                        docker.build("${DOCKER_IMAGE}:${DOCKER_TAG}")
                    }
                }
            }
        }
        
        stage('Push Docker Image') {
            steps {
                script {
                    withDockerRegistry(credentialsId: DOCKER_CREDENTIALS_ID, toolName: DOCKER_TOOL) {
                        sh "docker push ${DOCKER_IMAGE}:${DOCKER_TAG}"
                    }
                }
            }
        }
    }

    post {
        success {
            echo 'Docker image successfully built and pushed!'
        }
        failure {
            echo 'There was a failure in the pipeline.'
        }
    }
}
