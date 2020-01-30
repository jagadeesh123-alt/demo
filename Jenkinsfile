pipeline {
  agent none
  stages {
    stage('Maven Install') {
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
        sh 'docker build -t demo/spring-petclinic1:latest .'
      }
    }
    stage('Docker Push') {
      agent any
      steps {
        docker.withRegistry('995966766395.dkr.ecr.us-east-1.amazonaws.com/demo', 'ecr:us-east-1:demo-ecr-credentials') {
          sh 'docker push girishsajjanar/spring-petclinic1:latest'
          sh 'docker image pull spring-petclinic1'
          sh 'docker run -d -p 9191:8080 spring-petclinic1'
        }
      }
    }
  }
}
