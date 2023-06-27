pipeline {
    agent any

    environment {
        AWS_REGION = 'us-east-1'
        ECR_REGISTRY_URL = '854171615125.dkr.ecr.us-east-1.amazonaws.com'
        DOCKER_IMAGE_NAME = 'deepanshurawat6-detection-model'
        DOCKER_IMAGE_TAG = '0.1.0'
        PATH = "./yolo5"
    }
    stages {
        stage('Checkout') {
            steps{
                git 'https://github.com/deepanshu-rawat6/App-Development-I.git'
            }
        }
        stage('Connecting with AWS') {
            steps{
                sh 'aws ecr get-login-password --region us-east-1 | docker login --username AWS --password-stdin 854171615125.dkr.ecr.us-east-1.amazonaws.com'
            }
        }
        stage('Building docker image') {
            steps{
                 sh 'docker build -t deepanshurawat6-detection-model ./yolo5'
            }
        }
        stage('Tagging the image') {
            steps{
                sh 'docker tag deepanshurawat6-detection-model:0.1.0 854171615125.dkr.ecr.us-east-1.amazonaws.com/deepanshurawat6-detection-model:0.1.0'
            }
        }
        stage('Pushing to ECR') {
            steps {
                sh 'docker push 854171615125.dkr.ecr.us-east-1.amazonaws.com/deepanshurawat6-detection-model:0.1.0'
            }
        }
        stage('Finished with Yolo5 app') {
            steps {
                sh '''
                        echo "Finished with Yolo5 app"
                '''
            }
        }
    }
}