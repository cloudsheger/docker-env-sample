pipeline {
    agent any
    options{
        buildDiscarder(logRotator(numToKeepStr: '5', daysToKeepStr: '5'))
        timestamps()
    }

    environment {
    //registry = "YourDockerhubAccount/YourRepository"
    registry = "cloudsheger/jenkins"
    registryCredential = 'DockerID'
    dockerImage = ''
    //registry = "<dockerhub-username>/<repo-name>"
    //registryCredential = '<dockerhub-credential-name>'
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
                 app = docker.build("docker-env-ami")
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
                    docker.withRegistry('https://registry.hub.docker.com', 'DockerID') {
                    app.push("${env.BUILD_NUMBER}")
                    app.push("latest")
                    }
                }
            }
        }
    }
}
