pipeline {
    agent any

    environment {
        IMAGE_NAME = 'sjagdale616/frontend'
        IMAGE_TAG = "${env.BUILD_NUMBER}"
        DOCKER_CREDENTIALS_ID = 'docker-cred'
    }

    stages {
        stage('Build & Tag Docker Image') {
            steps {
                script {
                    withDockerRegistry(credentialsId: "${env.DOCKER_CREDENTIALS_ID}", toolName: 'docker') {
                        sh "docker build -t ${env.IMAGE_NAME}:${env.IMAGE_TAG} ."
                    }
                }
            }
        }

        stage('Push Docker Image') {
            steps {
                script {
                    withDockerRegistry(credentialsId: "${env.DOCKER_CREDENTIALS_ID}", toolName: 'docker') {
                        sh "docker push ${env.IMAGE_NAME}:${env.IMAGE_TAG}"
                    }
                }
            }
        }

        stage('Update Latest Tag') {
            steps {
                script {
                    withDockerRegistry(credentialsId: "${env.DOCKER_CREDENTIALS_ID}", toolName: 'docker') {
                        sh """
                            docker tag ${env.IMAGE_NAME}:${env.IMAGE_TAG} ${env.IMAGE_NAME}:latest
                            docker push ${env.IMAGE_NAME}:latest
                        """
                    }
                }
            }
        }
    }

    post {
        always {
            script {
                // Cleanup: remove local Docker images to free up space
                sh """
                    docker rmi ${env.IMAGE_NAME}:${env.IMAGE_TAG} || true
                    docker rmi ${env.IMAGE_NAME}:latest || true
                """
            }
        }
    }
}
