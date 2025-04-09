pipeline {
    agent any

    environment {
        IMAGE_NAME = 'snadig/simple-flask-app'
        IMAGE_TAG = 'latest'
    }

    stages {
        stage('Checkout Code') {
            steps {
                git credentialsId: 'GitHub-PAT', url: 'https://github.com/SurakshaNadig/simple-flask-app.git', branch: 'main'
            }
        }

        stage('Build Docker Image') {
            steps {
                script {
                    // Make sure Docker is installed and available
                    sh 'docker --version' // To verify Docker is working
                    sh "docker build -t ${IMAGE_NAME}:${IMAGE_TAG} ."
                }
            }
        }

        stage('Push to Docker Hub') {
            steps {
                withCredentials([usernamePassword(credentialsId: 'Dockerhubcreds', usernameVariable: 'DOCKER_USER', passwordVariable: 'DOCKER_PASS')]) {
                    script {
                        // Make sure Docker is working
                        sh 'docker --version' // Check Docker status before login

                        sh """
                            echo "$DOCKER_PASS" | docker login -u "$DOCKER_USER" --password-stdin
                            docker push ${IMAGE_NAME}:${IMAGE_TAG}
                        """
                    }
                }
            }
        }
    }

    post {
        success {
            echo "✅ Build and push to Docker Hub succeeded!"
        }
        failure {
            echo "❌ Build or push failed. Check logs above for details."
        }
    }
}

