pipeline {
    agent any

    environment {
        DOCKER_IMAGE = 'snadi/simple-flask-app'
        DOCKER_TAG = 'latest'
    }

    stages {
        stage('Checkout SCM') {
            steps {
                git credentialsId: 'GitHub-PAT', url: 'https://github.com/SurakshaNadig/simple-flask-app.git', branch: 'main'
            }
        }

        stage('Build Docker Image') {
            steps {
                script {
                    docker.build("${DOCKER_IMAGE}:${DOCKER_TAG}")
                }
            }
        }

        stage('Push to Docker Hub') {
            steps {
                withCredentials([usernamePassword(credentialsId: 'Dockerhubcreds', usernameVariable: 'DOCKER_USER', passwordVariable: 'DOCKER_PASS')]) {
                    script {
                        sh 'echo $DOCKER_PASS | docker login -u $DOCKER_USER --password-stdin'
                        sh "docker push ${DOCKER_IMAGE}:${DOCKER_TAG}"
                    }
                }
            }
        }
    }

    post {
        success {
            echo "✅ Build and push completed successfully."
        }
        failure {
            echo "❌ Build failed. Check the logs for more details."
        }
    }
}

