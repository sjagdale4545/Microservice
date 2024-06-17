pipeline {
    agent any

    stages {
        stage('Deploy To Kubernetes') {
            steps {
                withKubeCredentials(
                    kubectlCredentials: [
                        [
                            credentialsId: 'k8-token',
                            serverUrl: 'https://44159A061A49CB4AE885E7F2445EE295.gr7.ap-south-1.eks.amazonaws.com',
                            clusterName: 'EKS-1',
                            namespace: 'webapps',
                            caCertificate: '',
                            contextName: ''
                        ]
                    ]
                ) {
                    sh "kubectl apply -f deployment-service.yml"
                }
            }
        }

        stage('Verify Deployment') {
            steps {
                withKubeCredentials(
                    kubectlCredentials: [
                        [
                            credentialsId: 'k8-token',
                            serverUrl: 'https://44159A061A49CB4AE885E7F2445EE295.gr7.ap-south-1.eks.amazonaws.com',
                            clusterName: 'EKS-1',
                            namespace: 'webapps',
                            caCertificate: '',
                            contextName: ''
                        ]
                    ]
                ) {
                    sh "kubectl get svc -n webapps"
                }
            }
        }
    }
}
