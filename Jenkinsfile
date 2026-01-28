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

        stage('Check & Install Docker') {
            steps {
                sh '''
                if ! command -v docker >/dev/null 2>&1; then
                  echo "Docker not found. Installing..."
                  sudo apt update -y
                  sudo apt install -y docker.io
                  sudo systemctl start docker
                  sudo systemctl enable docker
                  sudo usermod -aG docker ubuntu
                else
                  echo "Docker already installed"
                fi
                docker --version
                '''
            }
        }

        stage('Build Docker Image') {
            steps {
                sh '''
                echo "Building Docker image from Dockerfile"
                sudo docker build -t $IMAGE_NAME .
                '''
            }
        }

        stage('Run Container') {
            steps {
                sh '''
                echo "Removing old container if exists"
                sudo docker rm -f $CONTAINER_NAME || true

                echo "Running container"
                sudo docker run -d \
                  --name $CONTAINER_NAME \
                  -p 80:80 \
                  $IMAGE_NAME

                sudo docker ps
                '''
            }
        }
    }
}
