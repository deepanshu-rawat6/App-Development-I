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
        stage('Build') {
            steps {
                withEnv(['PATH+EXTRA=/usr/sbin:/usr/bin:/sbin:/bin']) {
                    sh 'echo "Hello World"'
                    sh '''
                        echo "Multiline shell steps works too"
                        ls -lah
                    '''
                }
            }
        }
        // stage('Checking on env') {
        //     steps{
        //         sh '''
        //         echo "AWS_REGION: ${AWS_REGION}"
        //         echo "ECR_REGISTRY_URL: ${ECR_REGISTRY_URL}"
        //         echo "DOCKER_IMAGE_NAME: ${DOCKER_IMAGE_NAME}"
        //         echo "DOCKER_IMAGE_TAG: ${DOCKER_IMAGE_TAG}"
        //         echo "PATH: ${PATH}"
        //         '''
        //     }
        // }
        // stage('Connecting with AWS') {
        //     steps{
        //         sh 'aws ecr get-login-password --region ${AWS_REGION} | docker login --username AWS --password-stdin ${ECR_REGISTRY_URL}'
        //     }
        // }
        // stage('Building docker image') {
        //     steps{
        //          sh 'docker build -t ${DOCKER_IMAGE_NAME} ${PATH}'
        //     }
        // }
        // stage('Tagging the image') {
        //     steps{
        //         sh 'docker tag ${DOCKER_IMAGE_NAME}:${DOCKER_IMAGE_TAG} ${ECR_REGISTRY_URL}/${DOCKER_IMAGE_NAME}:${DOCKER_IMAGE_TAG}'
        //     }
        // }
        // stage('Pushing to ECR') {
        //     steps {
        //         sh 'docker push ${ECR_REGISTRY_NAME}/${DOCKER_IMAGE_NAME}:${DOCKER_IMAGE_TAG}'
        //     }
        // }
    }
}