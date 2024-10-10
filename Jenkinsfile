node('appserver')
{
    def app
    stage("Cloning Git")
    {
        checkout scm
    }

    stage("Build-and-Tag")
    {
        app = docker.build('widmatg/car_docker_web_repo')
    }

    stage("Post-to-Dockerhub")
    {
        docker.withRegistry('https://registry.hub.docker.com', 'dockerhub_credentials')
        {
            app.push('latest')
        }
    }

    stage("Deploy")
    {
        sh "docker-compose down"
        sh "docker-compose up -d"
    }
}