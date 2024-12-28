pipeline {
    agent any
    environment {
        DOCKER_IMAGE = "coffeshop/coffeshop:latest"
        DOCKER_CONTAINER = "coffeshop_project"
        PORT_MAPPING = "8089:80"
    }

    stages{
       stage("Clone Repository") {
            steps {
                deleteDir()
                checkout([$class: 'GitSCM', 
                          branches: [[name: '*/main']], 
                          userRemoteConfigs: [[url: 'https://github.com/ramadhanadi/coffeshop.git']]
                ])
            }
        }
        stage("build Docker Image"){
            steps{
                script{
                    docker.build(env.DOCKER_IMAGE)
                }
            }
        }
        stage("Run Docker Container"){
            steps{
                script{
                    docker.image(env.DOCKER_IMAGE).run("-d --name ${env.DOCKER_CONTAINER} -p ${env.PORT_MAPPING}")
                }
            }
        }
    }
}
