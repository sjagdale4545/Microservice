pipeline {
    agent any

    stages {
        stage('Delete Docker Image from Docker Hub') {
            steps {
                script {
                    def dockerHubUsername = 'sjagdale616'
                    def dockerHubRepository = 'frontend'
                    def dockerHubToken = 'dckr_pat_MPhIUa80Tx-HWPgA8cB1W4gvGF0'

                    sh """
                    curl -s -X DELETE -H "Authorization: JWT ${dockerHubToken}" \ 
                        https://hub.docker.com/v2/repositories/${dockerHubUsername}/${dockerHubRepository}/tags/latest/
                    """
                }
            }
        }

        stage('Build & Tag Docker Image') {
            steps {
                script {
                    withDockerRegistry(credentialsId: 'docker-cred', toolName: 'docker') {
                        sh "docker build -t sjagdale616/frontend:latest ."
                    }
                }
            }
        }
        
        stage('Push Docker Image') {
            steps {
                script {
                    withDockerRegistry(credentialsId: 'docker-cred', toolName: 'docker') {
                        sh "docker push sjagdale616/frontend:latest"
                    }
                }
            }
        }
    }
}
