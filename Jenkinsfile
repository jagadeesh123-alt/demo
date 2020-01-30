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
        sh 'sudo docker build -t jagdeesh123-alt/spring-petclinic1:latest .'
      }
    }
    stage('Docker Push') {
      agent any
      steps {
        withCredentials([usernamePassword(credentialsId: 'docker-hub', passwordVariable: 'dockerHubPassword', usernameVariable: 'dockerHubUser')]) {
          sh "sudo docker login -u ${env.dockerHubUser} -p ${env.dockerHubPassword}"
          sh 'sudo docker push jagdeesh123-alt/spring-petclinic1:latest'
          sh 'sudo docker image pull spring-petclinic1'
          sh 'sudo docker run -d -p 9191:8080 spring-petclinic1'
        }
      }
    }
  }
}
