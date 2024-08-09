pipeline {
    agent any

    environment {
        DOCKER_CREDENTIALS_ID = 'dockerhub_credentials'
        DOCKER_IMAGE = 'jespergmol/sn-midserver'
    }

    stages {
        stage('Checkout') {
            steps {
                git credentialsId: 'Github', branch: 'main', url: 'https://github.com/Arc86/sn-midserver.git'
            }
        }

        stage('Build Docker Image') {
            steps {
                script {
                    dockerImage = docker.build("${env.DOCKER_IMAGE}:latest")
                }
            }
        }

        stage('Push to Docker Hub') {
            steps {
                //snDevOpsChange()
                script {
                    docker.withRegistry('https://index.docker.io/v1/', "${env.DOCKER_CREDENTIALS_ID}") {
                        dockerImage.push()
                    }
                }
            }
        }
    }
}
