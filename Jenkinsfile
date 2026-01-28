pipeline {
    agent any

    environment {
        IMAGE_NAME = "cow-website-image"
        CONTAINER_NAME = "cow-website"
    }

    stages {

        stage('Checkout Code') {
            steps {
                git branch: 'main',
                    url: 'https://github.com/vaibhavkolase20/cow-website.git'
            }
        }

        stage('Verify Docker') {
            steps {
                sh '''
                docker --version
                docker ps
                '''
            }
        }

        stage('Build Docker Image') {
            steps {
                sh '''
                docker build -t $IMAGE_NAME .
                '''
            }
        }

        stage('Run Container') {
            steps {
                sh '''
                docker rm -f $CONTAINER_NAME || true

                docker run -d \
                  --name $CONTAINER_NAME \
                  -p 80:80 \
                  $IMAGE_NAME

                docker ps
                '''
            }
        }
    }
}
