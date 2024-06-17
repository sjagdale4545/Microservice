def isMainBranch = env.BRANCH_NAME == 'main'

pipeline {
    agent any

    stages {
        stage('Run on Main Branch Only') {
            when {
                expression {
                    return isMainBranch
                }
            }
        }
        stage('Deploy To Kubernetes') {
            steps {
                withKubeCredentials(kubectlCredentials: [[caCertificate: '', clusterName: 'EKS-1', contextName: '', credentialsId: 'k8-token', namespace: 'webapps', serverUrl: 'https://44159A061A49CB4AE885E7F2445EE295.gr7.ap-south-1.eks.amazonaws.com']]) {
                sh "kubectl apply -f deployment-service.yml"
                }
            }
        }
        stage('verify Deployment') {
            steps {
                withKubeCredentials(kubectlCredentials: [[caCertificate: '', clusterName: 'EKS-1', contextName: '', credentialsId: 'k8-token', namespace: 'webapps', serverUrl: 'https://44159A061A49CB4AE885E7F2445EE295.gr7.ap-south-1.eks.amazonaws.com']]) {
                sh "kubectl get svc -n webapps"
                }
            }
        }
    }
}
