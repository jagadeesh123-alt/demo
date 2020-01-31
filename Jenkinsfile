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
    stage('Build And Push Docker Image') {
    node('master'){
        docker.withRegistry('https://995966766395.dkr.ecr.us-west-2.amazonaws.com', 'ecr:us-west-2:access_id') {
           
            //build image
            def customImage = docker.build("995966766395.dkr.ecr.us-west-2.amazonaws.com/payvoo-ecr:demo")
             
            //push image
            customImage.push()
        }
    }
  }
  }
}
