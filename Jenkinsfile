pipeline {
    agent any

    environment {
        IMAGE_NAME = "devops-html-app"
        CONTAINER_NAME = "devops-html-container"
        PORT = "9090"
        DOCKER = "/usr/local/bin/docker"
    }

    stages {

        stage('Build Docker Image') {
            steps {
                sh '$DOCKER build -t $IMAGE_NAME .'
            }
        }

        stage('Run Container') {
            steps {
                sh '''
                $DOCKER rm -f $CONTAINER_NAME || true
                $DOCKER run -d -p $PORT:80 --name $CONTAINER_NAME $IMAGE_NAME
                '''
            }
        }

        stage('Terraform Init') {
            steps {
                sh '''
                cd terraform
                terraform init
                '''
            }
        }

        stage('Terraform Apply') {
            steps {
                sh '''
                cd terraform
                terraform apply -auto-approve
                '''
            }
        }
    }
}