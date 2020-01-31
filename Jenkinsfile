pipeline {
    agent none
    stages {
        stage('Build Jar') {
            agent {
                docker {
                    image 'maven:3-alpine'
                    args '-v $HOME/.m2:/root/.m2'
                }
            }
            steps {
                sh 'mvn clean package -DskipTests'
            }
        }
        stage('Build Image') {
            steps {
                script {
                    app = docker.build("995966766395.dkr.ecr.us-west-2.amazonaws.com/payvoo-ecr")
                }
            }
        }
        stage('Push Image') {
            steps {
                script {
                   app=docker.push("payvoo-ecr")
                }
            }
        }
    }
}
