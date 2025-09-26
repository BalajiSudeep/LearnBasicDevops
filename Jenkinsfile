pipeline {
    agent any

    environment {
        IMAGE_NAME = "balajisudeep/python-app"
        CONTAINER_NAME = "python-app"
    }

    stages {

        stage('Checkout') {
            steps {
                git branch: 'main',
                    url: 'https://github.com/BalajiSudeep/LearnBasicDevops.git'
            }
        }

        stage('Build Docker Image') {
            steps {
                sh "docker build -t ${IMAGE_NAME} ."
            }
        }

        stage('Run Container') {
            steps {
                sh '''
                    docker rm -f ${CONTAINER_NAME} || true
                    docker run -d --name ${CONTAINER_NAME} -p 5000:5000 ${IMAGE_NAME}
                '''
            }
        }

        stage('Test Application') {
            steps {
                sh "docker ps | grep ${CONTAINER_NAME}"
            }
        }

        // Optional Cleanup
        stage('Cleanup') {
            steps {
                echo "Cleanup skipped for now."
            }
        }
    }

    post {
        always {
            echo "Pipeline execution finished."
        }
    }
}
