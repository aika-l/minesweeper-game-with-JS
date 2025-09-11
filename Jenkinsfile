pipeline {
    agent any

    environment {
        IMAGE_NAME = "ailitik/minesweeper"
        DOCKERHUB_CREDS = credentials('c7bce02b-5052-4912-8872-161dff4ea527')
    }

    stages {
        stage('Clone Repo') {
            steps {
                git branch: 'main', url: 'https://github.com/aika-l/minesweeper-game-with-JS.git'
            }
        }

        stage('Build Docker Image') {
            steps {
                script {
                    sh """
                        docker build -t $IMAGE_NAME:latest .
                    """
                 }
            }
        }

        stage('Push to Docker Hub') {
            steps {
                script {
                    sh """
                        echo $DOCKERHUB_CREDS_PSW | docker login -u $DOCKERHUB_CREDS_USR --password-stdin
                        docker push $IMAGE_NAME:latest
                    """
                }
            }
        }
    }
}
