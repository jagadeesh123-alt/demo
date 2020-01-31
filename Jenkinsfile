node {
    def app
    stage('Clone repository') {
        /* Let's make sure we have the repository cloned to our workspace */
        checkout scm
    }
    stage('Build Web image') {
        /* This builds the actual image; synonymous to
         * docker build on the command line */
        app = docker.build("web",".source/Web/Dockerfile")
    }
    stage('Test image') {
        /* Ideally, we would run a test framework against our image.
         * For this example, we're using a Volkswagen-type approach ;-) */
        app.inside {
            sh 'echo "Tests passed"'
        }
    }
    stage('Push image') {
        /* Finally, we'll push the image with two tags:
         * First, the incremental build number from Jenkins
         * Second, the 'latest' tag.
         * Pushing multiple tags is cheap, as all the layers are reused. */
        docker.withRegistry('995966766395.dkr.ecr.us-west-2.amazonaws.com', 'payvoo-ecr:docker-hub-credentials') {
            docker.image('web').push('latest')
            /*app.push("${env.BUILD_NUMBER}")
            app.push("latest")*/
        }
    }
}
