stage('Build And Push Docker Image') {
    node('master'){
        docker.withRegistry('https://us-west-2.console.aws.amazon.com/ecr/repositories?region=us-west-2', 'ecr:us-west-2:access_id') {
           
            //build image
            def customImage = docker.build("995966766395.dkr.ecr.us-west-2.amazonaws.com/payvoo-ecr:latest")
             
            //push image
            customImage.push()
        }
    }
  }
