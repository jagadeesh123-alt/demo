try {
  stage('Clone Repo'){
    node('master'){
      checkout([$class: 'GitSCM', branches: [[name: '*/jaga']], doGenerateSubmoduleConfigurations: false, extensions: [], submoduleCfg: [], userRemoteConfigs: [[url: 'https://github.com/jagadeesh123-alt/demo.git']]])
    }
  }
  stage('Build Maven'){
    node('master'){
       sh "mvn clean install"
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
catch (err){
  currentBuild.result = "FAILURE"
  throw err
}
