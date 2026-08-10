pipeline {
    agent any

    stages {
        stage('Deploy To Kubernetes') {
            steps {
                withKubeCredentials(kubectlCredentials: [[caCertificate: '', clusterName: 'EKS-2', contextName: '', credentialsId: 'k8-token', namespace: 'webapps', serverUrl: 'https://F7F952F0424FBD2EA07B6A9EE793B9B0.gr7.us-east-1.eks.amazonaws.com']]) {
                    sh "kubectl apply -f deployment-service.yml"
                    
                }
            }
        }
        
        stage('verify Deployment') {
            steps {
                withKubeCredentials(kubectlCredentials: [[caCertificate: '', clusterName: 'EKS-1', contextName: '', credentialsId: 'k8-token', namespace: 'webapps', serverUrl: 'https://F7F952F0424FBD2EA07B6A9EE793B9B0.gr7.us-east-1.eks.amazonaws.com']]) {
                    sh "kubectl get svc -n webapps"
                }
            }
        }
    }
}
