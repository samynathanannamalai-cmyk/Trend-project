pipeline {
    agent any

    environment {
        IMAGE_NAME = "annamalaiaws/trend-app"
    }

    stages {

        stage('Clone Repo') {
            steps {
                git branch: 'main',
                url: 'https://github.com/samynathanannamalai-cmyk/Trend-project.git'
            }
        }

        stage('Build Docker Image') {
            steps {
                sh 'docker build -t $IMAGE_NAME:latest .'
            }
        }

        stage('Push to DockerHub') {
            steps {
                withDockerRegistry(credentialsId: 'dockerhub-creds', url: '') {
                    sh 'docker push $IMAGE_NAME:latest'
                }
            }
        }

        stage('Deploy to EKS') {
            steps {
                sh 'kubectl apply -f deployment.yaml'
                sh 'kubectl apply -f service.yaml'
            }
        }
    }
}
