pipeline {
    agent any

    environment {
        IMAGE_NAME = "devops-html-app"
        CONTAINER_NAME = "devops-html-container"
        PORT = "9090"
    }

    stages {

        stage('Clone Code') {
            steps {
                git 'https://github.com/Sr-Gaurav/devopsexp.git'
            }
        }

        stage('Build Docker Image') {
            steps {
                sh 'docker build -t $IMAGE_NAME .'
            }
        }

        stage('Run Container') {
            steps {
                sh '''
                docker rm -f $CONTAINER_NAME || true
                docker run -d -p 3000:3000 --name $CONTAINER_NAME $IMAGE_NAME
                '''
            }
        }
    }
}