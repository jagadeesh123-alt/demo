pipeline {
  agent none
  stages {
    stage('Docker Install') {
      agent {
        docker {
          image 'docker:stable'
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
        withCredentials([usernamePassword(credentialsId: 'docker-hub', passwordVariable: 'dockerHubPassword', usernameVariable: 'dockerHubUser')]) {
          sh "docker login -u ${env.dockerHubUser} -p ${env.dockerHubPassword}"
          sh 'docker push girishsajjanar/spring-petclinic1:latest'
          sh 'docker image pull spring-petclinic1'
          sh 'docker run -d -p 9191:8080 spring-petclinic1'
        }
      }
    }
  }
}
