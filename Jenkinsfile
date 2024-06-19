pipeline {
    agent any

    environment {
        DOCKER_IMAGE = 'sjagdale616/frontend'
        DOCKER_TAG = 'latest2'
    }

    stages {
        stage('Build & Tag Docker Image') {
            steps {
                script {
                    withDockerRegistry(credentialsId: 'docker-cred', toolName: 'docker') {
                        sh "docker build --no-cache -t ${DOCKER_IMAGE}:${DOCKER_TAG} ."
                    }
                }
            }
        }
        
        stage('Push Docker Image') {
            steps {
                script {
                    withDockerRegistry(credentialsId: 'docker-cred', toolName: 'docker') {
                        sh "docker push ${DOCKER_IMAGE}:${DOCKER_TAG}"
                    }
                }
            }
        }
    }
    
    post {
        always {
            script {
                try {
                    build job: 'main', wait: false
                } catch (Exception e) {
                    echo "Failed to trigger 'main' job: ${e.getMessage()}"
                }
            }
        }
    }
}
