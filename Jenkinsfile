pipeline {
    agent any

    environment {
        DOCKERHUB_CREDENTIALS = credentials('docker')
        IMAGE_NAME = 'snadig/flask-demo-private'
	GITHUB_NAME = 'https://github.com/SurakshaNadig/simple-flask-app1.git'
    }

    stages {
        // stage('Checkout Code') {
        //     steps {
        //         git clone {GITHUB_NAME}
        //     }
        // }

        stage('Build Docker Image') {
            steps {
                script {
                    sh 'docker build -t snadig/flask-demo-private:latest .'
                }
            }
        }

    }
}

