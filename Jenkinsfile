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
                script {
                    docker.build(IMAGE_NAME)
                }
            }
        }

        stage('Stop Old Container') {
            steps {
                script {
                    sh "docker rm -f ${CONTAINER_NAME} || true"
                }
            }
        }

        stage('Deploy Container') {
            steps {
                script {
                    docker.image(IMAGE_NAME).run("-d -p 80:80 --name ${CONTAINER_NAME}")
                }
            }
        }
    }

    post {
        success {
            echo "Deployment Successful! Visit http://<server-ip>"
        }
        failure {
            echo "Deployment failed."
        }
    }
}