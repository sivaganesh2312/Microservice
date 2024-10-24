pipeline {
    agent any

    tools {
    git 'Default'
    }

    stages {
        stage('Deploy To Kubernetes') {
            steps {
                withKubeCredentials(kubectlCredentials: [[caCertificate: '', clusterName: 'kubectl', contextName: '', credentialsId: 'k8-cred', namespace: 'webapps', serverUrl: 'https://10.138.0.7:6443']]) {
                    sh "kubectl apply -f deployment-service.yml"
                    
                }
            }
        }
        
        stage('verify Deployment') {
            steps {
                withKubeCredentials(kubectlCredentials: [[caCertificate: '', clusterName: 'kubectl', contextName: '', credentialsId: 'k8-cred', namespace: 'webapps', serverUrl: 'https://10.138.0.7:6443']]) {
                    sh "kubectl get svc -n webapps"
                }
            }
        }
    }
}
