pipeline {
    agent any

    stages { 
        stage('Build & Tag Docker Image') {
            steps {
                script {
                    withDockerRegistry(credentialsId: 'docker-cred', toolName: 'docker') {
                        sh "docker build -t sjagdale616/frontend2 ."
                    }
                }
            }
        } 
        stage('Push Docker Image') {
            steps {
                script {
                    withDockerRegistry(credentialsId: 'docker-cred', toolName: 'docker') {
                        sh "docker push sjagdale616/frontend2"
                    }
                }
            }
        }
         stage('Run on Main Branch Only') {
            when {
                expression {
                    env.BRANCH_NAME == 'main'
                }
            }
    }
}
