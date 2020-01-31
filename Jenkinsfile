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
                    docker.build('payvoo')
                }
            }
        }
        stage('Push Image') {
            steps {
                docker.withRegistry('https://995966766395.dkr.ecr.us-west-2.amazonaws.com', 'ecr:us-west-2:payvoo-ecr-credentials')
                script {
                   docker.image('payvoo').push('latest')
                }
            }
        }
    }
}
