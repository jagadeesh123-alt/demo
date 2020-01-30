pipeline {
  agent none
  stages {
    stage('Docker Install') {
      agent {
        docker {
          image 'maven:3.5.0'
        }
      }
      steps {
        sh 'mvn clean install'
      }
    }
    stage('Docker Build') {
      agent any
      steps {
        sh 'docker build -t girishsajjanar/spring-petclinic1:latest .'
      }
    }
    stage('Docker Push') {
      agent any
      steps {
        docker.withRegistry('https://995966766395.dkr.ecr.us-east-1.amazonaws.com/demo', 'ecr:us-east-1:demo-ecr-credentials') {
          docker.image('demo').push('latest')
        }
      }
    }
  }
}
