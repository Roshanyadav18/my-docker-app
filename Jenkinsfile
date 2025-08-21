pipeline {
    agent any

    environment {
        DOCKERHUB_CREDENTIALS = credentials('dockerhub-creds')
        IMAGE_NAME = "roshanyadav18/my-docker-app"
    }

    stages {
        stage('Clone Code') {
            steps {
                git branch: 'main', url: 'git@github.com:Roshanyadav18/my-docker-app.git'
            }
        }

        stage('Run Tests') {
            steps {
                echo "Running tests..."
                // Example test: check if index.html file exists
                sh 'test -f index.html'
            }
        }

        stage('Build Docker Image') {
            steps {
                sh "docker build -t $IMAGE_NAME:${BUILD_NUMBER} ."
            }
        }

        stage('Push to DockerHub') {
            steps {
                sh "echo $DOCKERHUB_CREDENTIALS_PSW | docker login -u $DOCKERHUB_CREDENTIALS_USR --password-stdin"
                sh "docker push $IMAGE_NAME:${BUILD_NUMBER}"
            }
        }

        stage('Deploy Container') {
            steps {
                sh "docker rm -f my-docker-app || true"
                sh "docker run -d --name my-docker-app -p 9090:80 $IMAGE_NAME:${BUILD_NUMBER}"
            }
        }
    }
}
