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
                sh 'aws ecr get-login-password --region ${AWS_REGION} | docker login --username AWS --password-stdin ${ECR_REGISTRY_URL}'
            }
        }
        stage('Building docker image') {
            steps{
                 sh 'docker build -t ${DOCKER_IMAGE_NAME} ${PATH}'
            }
        }
        stage('Tagging the image') {
            steps{
                sh 'docker tag ${DOCKER_IMAGE_NAME}:${DOCKER_IMAGE_TAG} ${ECR_REGISTERY_URL}/${DOCKER_IMAGE_NAME}:${DOCKER_IMAGE_TAG}'
            }
        }
        stage('Pushing to ECR') {
            steps {
                sh 'docker push ${ECR_REGISTRY_URL}/${DOCKER_IMAGE_NAME}:${DOCKER_IMAGE_TAG}'
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