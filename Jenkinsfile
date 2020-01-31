pipeline
{
    options
    {
        buildDiscarder(logRotator(numToKeepStr: '3'))
    }
 
    agent any
    environment 
    {
        PROJECT = 'tap_sample'
        ECRURL = 'http://995966766395.dkr.ecr.us-west-2.amazonaws.com'
        ECRCRED = 'ecr:us-west-2:payvoo-ecr'
    }
    stages
    {
        stage('Docker image pull')
        {
            steps
            {
                script
                {
                    sh("eval \$(aws ecr get-login --no-include-email | sed 's|https://http://995966766395.dkr.ecr.us-west-2.amazonaws.com||')")
                    docker.withRegistry(ECRURL, ECRCRED)
                    {
                        docker.image(PROJECT).pull()
                    }
                }
            }
        }
    }
}
