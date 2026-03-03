pipeline {
    agent any

    environment {
        IMAGE_NAME = "mywebsite"
    }

    stages {

        stage('Clone Code') {
            steps {
                git 'https://github.com/yourusername/yourrepo.git'
            }
        }

        stage('Build Docker Image') {
            steps {
                sh 'docker build -t $IMAGE_NAME .'
            }
        }

        stage('Stop Old Container') {
            steps {
                sh 'docker stop website || true'
                sh 'docker rm website || true'
            }
        }

        stage('Run New Container') {
            steps {
                sh 'docker run -d -p 8080:80 --name website $IMAGE_NAME'
            }
        }
    }
}