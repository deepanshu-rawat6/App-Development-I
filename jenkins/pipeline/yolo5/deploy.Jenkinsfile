pipeline {
    agent {
    docker {
            // label 'jenkins_agent'
            image '854171615125.dkr.ecr.us-east-1.amazonaws.com/deepanshurawat6-jenkins-agent:3.2.0'
            args  '--user root -v /var/run/docker.sock:/var/run/docker.sock'
        }
    }

    parameters { string(name: 'YOLO5_IMAGE_URL', defaultValue: '', description: '') }
    
    environment {
        AWS_REGION_K8S = 'us-east-2'
        K8S_CLUSTER_NAME = 'k8s-batch1'
        K8S_NAMESPACE = 'deepanshu-rawat6'
        MANIFEST_FILE = 'yolo5-deployment.yaml'
    }
    stages {
        stage('Staring the deploy process') {
            steps {
                    sh 'echo "Starting off the deploy process"'
            }
        }
        stage('Connecting to the k8s cluster') {
            steps {
                    sh 'aws eks --region ${AWS_REGION_K8S} update-kubeconfig --name ${K8S_CLUSTER_NAME}'
            }
        }
        stage('Setting default namespace') {
            steps {
                    sh 'kubectl config set-context --current --namespace=${K8S_NAMESPACE}'
            }
        }
        stage('Deploying on k8s') {
            steps {
                   sh '''
                        cd "k8s"

                        kubectl apply -f ${MANIFEST_FILE}
                   '''
            }
        }
        stage('Finishing the deploy process') {
            steps {
                   sh 'echo "Finishing off the deploy process" '
            }
        }
    }
}