pipeline {
    agent any

    environment {
        IMAGE_NAME = "ci-cd-local-app"
    }

    stages {

        stage('Git Checkout') {
            steps {
                git 'https://github.com/Sodhu1008/devops-ci-cd-local.git'
            }
        }

        stage('Build Docker Image') {
            steps {
                sh 'docker build -t $IMAGE_NAME .'
            }
        }

        stage('Stop Old Container') {
            steps {
                sh 'docker stop local-app || true'
                sh 'docker rm local-app || true'
            }
        }

        stage('Run New Container') {
            steps {
                sh 'docker run -d -p 3000:3000 --name local-app $IMAGE_NAME'
            }
        }
    }
}
