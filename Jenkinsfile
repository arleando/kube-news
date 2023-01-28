pipeline {
    agent any

    stages {

        stage('Bild Docker Image') {
            steps {
                script{
                    dockerapp = docker.build("arleando/kube-news:${env.BUILD_ID}", '-f ./src/Dockerfile ./src')
                }
            }

        }   
        stage('Push Docker Image') {
            steps {
                script{
                    docker.withRegistry('https://registry.hub.docker.com', 'dockerhub') {
                        dockerapp.push('latest')
                        dockerapp.push("${env.BUILD_ID}")
                    }
                        
                }
            }
        }
        stage('Deploy Kubernetes'){
            steps{
                withKubeconfig ([credentialsId: 'kubeconfig1']){
                    sh 'kubectl apply -f ./k8s/deployment.yaml'
                }
            }
        }
    }
}
