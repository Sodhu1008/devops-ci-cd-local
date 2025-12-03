pipeline {
    agent any

    environment {
        IMAGE_NAME = "ci-cd-local-app"
    }

    stages {

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

    post {
        success {
            mail to: 'soudharmrlende@gmail.com',
                 subject: "✔ SUCCESS: '${env.JOB_NAME} #${env.BUILD_NUMBER}' Completed",
                 body: "Hello,\n\nYour Jenkins pipeline finished successfully.\n\nJob: ${env.JOB_NAME}\nBuild: ${env.BUILD_NUMBER}\nStatus: SUCCESS\n\nRegards,\nJenkins CI/CD"
        }

        failure {
            mail to: 'soudharmrlende@gmail.com',
                 subject: "❌ FAILURE: '${env.JOB_NAME} #${env.BUILD_NUMBER}' Failed",
                 body: "Hello,\n\nYour Jenkins pipeline has FAILED.\n\nJob: ${env.JOB_NAME}\nBuild: ${env.BUILD_NUMBER}\nStatus: FAILED\n\nCheck Jenkins console for more details.\n\nRegards,\nJenkins CI/CD"
        }
    }
}
