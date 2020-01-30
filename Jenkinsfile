node {
  stage 'Checkout'
  git 'git@github.com:jagadeesh123-alt/demo.git'
 
  stage 'Docker build'
  docker.build('demo')
 
  stage 'Docker push'
  docker.withRegistry('https://995966766395.dkr.ecr.us-east-1.amazonaws.com/demo', 'ecr:us-east-1:demo-ecr-credentials') {
    docker.image('demo').push('latest')
  }
}
