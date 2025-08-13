echo 'pipeline {
    agent any

    environment {
        DOCKERHUB_CREDS = credentials("dockerhub-creds")
        DOCKER_IMAGE = "roshanyadav18/my-docker-app"
    }

    stages {
        stage("Checkout") {
            steps {
                git branch: "main", url: "https://github.com/Roshanyadav18/my-docker-app.git"
            }
        }

        stage("Build Docker Image") {
            steps {
                script {
                    docker.build("${DOCKER_IMAGE}")
                }
            }
        }

        stage("Push to DockerHub") {
            steps {
                script {
                    docker.withRegistry("https://registry.hub.docker.com", "dockerhub-creds") {
                        docker.image("${DOCKER_IMAGE}").push("latest")
                    }
                }
            }
        }
    }
}' > Jenkinsfile
