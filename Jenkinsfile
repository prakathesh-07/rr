pipeline {
    agent any
    stages {
        stage('Checkout') {
            steps {
                git url: 'https://github.com/prakathesh-07/rr.git', branch: 'main'
            }
        }

        stage('Build Docker Image') {
            steps {
                script {
                    // Build the Docker image
                    docker.build('my-image-name:latest')
                }
            }
        }

        stage('Stop Old Container') {
            steps {
                script {
                    // Stop old container if running
                    sh "docker stop my-container || true"
                    sh "docker rm my-container || true"
                }
            }
        }

        stage('Deploy Container') {
            steps {
                script {
                    // Run new container
                    sh "docker run -d --name my-container -p 8080:8080 my-image-name:latest"
                }
            }
        }
    }
    post {
        failure {
            echo 'Deployment failed.'
        }
    }
}
            
