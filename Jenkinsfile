pipeline {
    agent any

    environment {
        IMAGE_NAME = "ziedmahjoub/monapp"
        IMAGE_TAG = "latest"
    }

    stages {

        stage('Build Docker Image') {
            steps {
                echo "Construction de l'image Docker..."
                script {
                    docker.build("${IMAGE_NAME}:${IMAGE_TAG}")
                }
            }
        }

        stage('Push Docker Image') {
            steps {
                echo "Push de l'image vers Docker Hub..."
                script {
                    docker.withRegistry('https://index.docker.io/v1/', 'dockerhub-cred') {
                        docker.image("${IMAGE_NAME}:${IMAGE_TAG}").push()
                    }
                }
            }
        }
    }
}
