pipeline {
    agent any

    environment {
        AWS_REGION = 'us-east-1'
        ECR_REGISTRY_URL = '854171615125.dkr.ecr.us-east-1.amazonaws.com'
        DOCKER_IMAGE_NAME = 'deepanshurawat6-detection-model'
        DOCKER_IMAGE_TAG = '0.1.0'
        PATH+EXTRA=/usr/sbin:/usr/bin:/sbin:/bin
        // PATH = '/var/lib/jenkins/workspace/Yolo5Build/yolo5'
    }
    stages {
        stage('Build') {
            steps {
                // script {    
                //     def newVersion = incremetVersion(DOCKER_IMAGE_TAG)
                //     echo "New  version: ${newVersion}"
                //     writeFile file: 'version.txt', text: newVersion
                // }
                // withEnv(['PATH+EXTRA=/usr/sbin:/usr/bin:/sbin:/bin']) {
                // }
                sh '''
                    echo "Starting off the build process"
                '''
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
        stage('Connecting with AWS CLI') {
            steps{
                    sh 'aws ecr get-login-password --region ${AWS_REGION} | docker login --username AWS --password-stdin ${ECR_REGISTRY_URL}'
            }
        }
        stage('Building docker image') {
            steps{
                    sh '''
                        cd "/var/lib/jenkins/workspace/Yolo5Build/yolo5"
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
    }
}

// def incremetVersion(DOCKER_IMAGE_TAG) {
//     def parts = DOCKER_IMAGE_TAG.split('\\.')
//     int major = parts[0] as int
//     int minor = parts[1] as int
//     int patch = parts[2] as int

//     minor++ 

//     if (minor == 10) {
//         major++
//         minor = 0
//         patch = 0
//     }

//     return "${major}.${minor}.${patch}"
}