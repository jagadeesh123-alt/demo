pipeline {
    agent any

    stages {
        stage('Build') {
            steps {
                bat  'docker build -t test-repository .'
            }
        }
        stage('Push image') {
         steps {
           withDockerRegistry([url: "https://995966766395.dkr.ecr.us-east-1.amazonaws.com/demo",credentialsId: "ecr:us-east-1:demo-ecr-credentials"]) {
           bat 'docker push sampleapp:latest'
               }
        }
        stage('Deploy') {
            steps {
                echo 'Deploying....'
            }
        }
    }
}
