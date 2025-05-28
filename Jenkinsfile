pipeline {
    agent any

    environment {
        IMAGE_NAME = 'pavithra/mean-app'
        TAG = 'latest'
    }

    stages {
        stage('Clone Repo') {
            steps {
                git 'https://github.com/linnovate/mean.git'
            }
        }

        stage('Build Docker Image') {
            steps {
                sh 'docker build -t $IMAGE_NAME:$TAG .'
            }
        }

        stage('Run Docker Container') {
            steps {
                sh '''
                    docker stop mean-container || true
                    docker rm mean-container || true
                    docker run -d --name mean-container -p 3000:3000 $IMAGE_NAME:$TAG
                '''
            }
        }
    }
}
