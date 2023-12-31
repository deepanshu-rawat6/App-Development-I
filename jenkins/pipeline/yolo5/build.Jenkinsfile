pipeline {
    agent {
    docker {
            // label 'jenkins_agent'
            image '854171615125.dkr.ecr.us-east-1.amazonaws.com/deepanshurawat6-jenkins-agent:3.2.0'
            args  '--user root -v /var/run/docker.sock:/var/run/docker.sock'
        }
    }
    environment {
        AWS_REGION = 'us-east-1'
        ECR_REGISTRY_URL = '854171615125.dkr.ecr.us-east-1.amazonaws.com'
        DOCKER_IMAGE_NAME = 'deepanshurawat6-detection-model'
        DOCKER_IMAGE_TAG = '0.1.0'
    }
    stages {
        stage('Starting Build') {
            steps {
                    sh 'echo "Starting off the build process"'
            }
        }
        stage('Checking on env') {
            steps{
                    sh '''
                        echo "AWS_REGION: ${AWS_REGION}"
                        echo "ECR_REGISTRY_URL: ${ECR_REGISTRY_URL}"
                        echo "DOCKER_IMAGE_NAME: ${DOCKER_IMAGE_NAME}"
                        echo "DOCKER_IMAGE_TAG: ${DOCKER_IMAGE_TAG}"
                    '''
            }
        }
        stage('Connecting with ECR') {
            steps{
                    sh 'aws ecr get-login-password --region ${AWS_REGION} | docker login --username AWS --password-stdin ${ECR_REGISTRY_URL}'
            }
        }
        stage('Building docker image') {
            steps{
                    sh '''
                        cd "yolo5"
                        docker build -t ${DOCKER_IMAGE_NAME}:${DOCKER_IMAGE_TAG} .
                    '''
            }
        }
        stage('Tagging the image') {
            steps{
                    sh 'docker tag ${DOCKER_IMAGE_NAME}:${DOCKER_IMAGE_TAG} ${ECR_REGISTRY_URL}/${DOCKER_IMAGE_NAME}:${DOCKER_IMAGE_TAG}'
            }
        }
        stage('Pushing to ECR') {
            steps {
                    sh 'docker push ${ECR_REGISTRY_URL}/${DOCKER_IMAGE_NAME}:${DOCKER_IMAGE_TAG}'
            }
        }
        stage('End Build') {
            steps {
                sh '''
                    echo "Done with the build process"
                '''
            }
        }
        stage('Trigger Deploy') {
            steps {
                build job: 'Yolo5Deploy', wait: false, parameters: [
                    string(name: 'YOLO5_IMAGE_URL', value: "${ECR_REGISTRY_URL}/${DOCKER_IMAGE_NAME}:${DOCKER_IMAGE_TAG}")
                ]
            }
        }
    }
}