pipeline {
    agent any

    stages {
        stage('Unittest') {
            stages{
                stage("Installing dependencies") {
                    steps {
                        sh 'cd yolo5'
                        sh 'pip install -r requirements.txt'
                    }
                }
                stage("Run testcases") {
                    steps {
                        sh 'cd tests'
                        sh 'python3 -m pytest --junitxml results.xml tests'
                    }
                    post {
                        always {
                            junit allowEmptyResults: true, testResults: 'results.xml'
                        }
                    }
                }

            }
        }
        stage('Lint') {
            steps {
                sh 'echo "linting"'
            }
        }
        stage('Functional test') {
            steps {
                sh 'echo "testing"'
            }
        }
    }
}