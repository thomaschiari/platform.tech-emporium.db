pipeline {
    agent any

    stages {
        stage('Deploy on k8s') {
            steps {
                withCredentials([ string(credentialsId: 'minikube_credentials', variable: 'api_token') ]) {
                    sh 'kubectl --token $api_token --server https://host.docker.internal:52764  --insecure-skip-tls-verify=true apply -f ./k8s/deployment.yaml '
                    sh 'kubectl --token $api_token --server https://host.docker.internal:52764  --insecure-skip-tls-verify=true apply -f ./k8s/service.yaml '
                }
            }
        }
    }

    post {
        success {
            echo 'Redis deployment completed successfully.'
        }
        failure {
            echo 'Redis deployment failed.'
        }
    }
}
