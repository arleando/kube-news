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
    
    }
}