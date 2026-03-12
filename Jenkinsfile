pipeline {
    agent any

    environment {
        IMAGE_NAME = "rr:latest"
        CONTAINER_NAME = "rr_container"
    }

    stages {

        stage('Clone Repository') {
            steps {
                git branch: 'main', url: 'https://github.com/prakathesh-07/rr.git'
            }
        }

        stage('Build Docker Image') {
            steps {
                sh "docker build -t ${IMAGE_NAME} ."
            }
        }

        stage('Stop Old Container') {
            steps {
                sh "docker rm -f ${CONTAINER_NAME} || true"
            }
        }

        stage('Deploy Container') {
            steps {
                sh "docker run -d -p 8081:80 --name ${CONTAINER_NAME} ${IMAGE_NAME}"
            }
        }

    }

    post {
        success {
            echo "Deployment Successful! Open http://localhost:8081"
        }
        failure {
            echo "Deployment failed."
        }
    }
}