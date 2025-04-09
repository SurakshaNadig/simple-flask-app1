pipeline {
    agent any

    environment {
        DOCKERHUB_CREDENTIALS = credentials('Dockerhubcreds')
        IMAGE_NAME = 'yourusername/flask-demo-private'
    }

    stages {
        stage('Checkout Code') {
            steps {
                git 'https://github.com/SurakshaNadig/simple-flask-app1'
            }
        }

        stage('Build Docker Image') {
            steps {
                script {
                    dockerImage = docker.build("${IMAGE_NAME}:${BUILD_NUMBER}")
                }
            }
        }

        stage('Push to Docker Hub') {
            steps {
                script {
                    docker.withRegistry('https://index.docker.io/v1/', 'Dockerhubcreds') {
                        dockerImage.push()
                    }
                }
            }
        }
    }
}

