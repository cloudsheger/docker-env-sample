pipeline {
    agent any

    environment {
    //registry = "YourDockerhubAccount/YourRepository"
    REGISTRY = "https://hub.docker.com/repositories/cloudsheger/"
    //registryCredential = 'dockerhub_id'
    //registryCredential = 'DockerID'
    REGISTRY_CREDENTIAL = 'DockerID'
    dockerImage = ''
    }

    options {
        skipStagesAfterUnstable()
    }
    stages {
         stage('Clone repository') { 
            steps { 
                script{
                checkout scm
                }
            }
        }

        stage('Build') { 
            steps { 
                script{
                 app = docker.build("DOCKER-ENV-AMI")
                }
            }
        }
        stage('Test'){
            steps {
                 echo 'Empty'
            }
        }
        stage('Deploy') {
            steps {
                script{
                    docker.withRegistry(${env.REGISTRY}, ${env.REGISTRY_CREDENTIAL}) {
                    app.push("${env.BUILD_NUMBER}")
                    app.push("latest")
                    }
                }
            }
        }
    }
}
