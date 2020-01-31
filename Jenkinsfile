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
        sh "docker build -t 995966766395.dkr.ecr.us-west-2.amazonaws.com/payvoo-ecr:latest ."
      }
    }
    stage('Docker Push') {
      agent any
      steps {
        withCredentials([usernamePassword(credentialsId: 'access_id', passwordVariable: 'dockerHubPassword', usernameVariable: 'dockerHubUser')]) {
          sh "eval \$(aws ecr get-login --no-include-email --region us-west-2 | sed 's|https://||')"
          sh "docker push 995966766395.dkr.ecr.us-west-2.amazonaws.com/payvoo-ecr:lates"
          sh "docker run -d -p 9191:8080 995966766395.dkr.ecr.us-west-2.amazonaws.com/payvoo-ecr:latest"
        }
      }
    }
  }
}
