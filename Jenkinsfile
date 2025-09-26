pipeline {
    agent any

    environment {
        IMAGE_NAME = "balajisudeep/python-app"
        CONTAINER_NAME = "python-app"
    }

    stages {

        stage('Checkout') {
            steps {
                git branch: 'main', url: 'https://github.com/BalajiSudeep/LearnBasicDevops.git'
            }
        }

        stage('Build Docker Image') {
            steps {
                script {
                    // Build Docker image
                    sh "docker build -t ${IMAGE_NAME} ."
                }
            }
        }

        stage('Run Container') {
            steps {
                script {
                    // Stop container if exists
                    sh "docker rm -f ${CONTAINER_NAME} || true"
                    // Run container
                    sh "docker run -d --name ${CONTAINER_NAME} -p 5000:5000 ${IMAGE_NAME}"
                }
            }
        }

        stage('Test Application') {
            steps {
                script {
                    // Example: check if app is running
                    sh "docker ps | grep ${CONTAINER_NAME}"
                }
            }
        }

        stage('Cleanup') {
            steps {
                script {
                    // Optional: remove container/image if you want
                    // sh "docker rm -f ${CONTAINER_NAME}"
                    // sh "docker rmi ${IMAGE_NAME}"
                }
            }
        }
    }

    post {
        always {
            echo "Pipeline execution finished."
        }
    }
}
