   stage('Docker Build') {
      agent any
      steps {
        sh 'docker build -t girishsajjanar/spring-petclinic1:demo .'
        sh "docker build -t 995966766395.dkr.ecr.us-west-2.amazonaws.com/payvoo-ecr:demo ."
      }
    }
    stage('Build And Push Docker Image') {
    node('master'){
        docker.withRegistry('https://995966766395.dkr.ecr.us-west-2.amazonaws.com', 'ecr:us-west-2:access_id') {

            //build image
            def customImage = docker.build("995966766395.dkr.ecr.us-west-2.amazonaws.com/payvoo-ecr:demo")

            //push image
            customImage.push()
    stage('Docker Push') {
      agent any
      steps {
        withCredentials([usernamePassword(credentialsId: 'access_id', passwordVariable: 'dockerHubPassword', usernameVariable: 'dockerHubUser')]) {
          sh "eval \$(aws ecr get-login --no-include-email --region us-west-2 | sed 's|https://||')"
          sh "docker push 995966766395.dkr.ecr.us-west-2.amazonaws.com/payvoo-ecr:lates"
          sh "docker run -d -p 9191:8080 995966766395.dkr.ecr.us-west-2.amazonaws.com/payvoo-ecr:demo"
        }
      }
    }
