node('ubuntu-appserver-3120') 
{
    def app
    stage('Cloning Git')
    {
    checkout scm
    }
    stage('Build-and-Tag')
    {
        /* This builds the actual images;
        * This is synonoymous to docker build on the command line */
        app =docker.build('kevinsasian/realestate_docker_repo')
    }
    stage('Post-to-dockerhub')
    {
        docker.withRegistry('https://registry.hub.docker.com', 'dockerhub_credentials')
        {
        app.push('latest')
        }    
    }

    stage('Pull-image-server')
    {
        sh 'docker-compose down'
        sh 'docker-compose up -d'

    }
}