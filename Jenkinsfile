pipeline {
    agent any

    environment {
        DOCKER_IMAGE = "vyshnavi525/my-app"  // change this
        IMAGE_TAG    = "${env.BUILD_NUMBER}"             // eg: 1, 2, 3...
    }

    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }

        stage('Build Docker Image') {
            steps {
                script {
                    echo "Building Docker image..."
                    dockerImage = docker.build("${DOCKER_IMAGE}:${IMAGE_TAG}")
                }
            }
        }

        stage('Push to Docker Hub') {
            steps {
                script {
                    echo "Pushing Docker image to Docker Hub..."
                    docker.withRegistry('https://index.docker.io/v1/', 'docker-hub-creds') {
                        dockerImage.push()          // pushes tag = BUILD_NUMBER
                        dockerImage.push("latest")  // also pushes latest
                    }
                }
            }
        }
    }
}
