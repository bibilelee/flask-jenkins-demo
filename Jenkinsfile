pipeline {
    agent any

    environment {
        IMAGE_NAME = 'flask-jenkins-demo'
        CONTAINER_NAME = 'flask-jenkins-demo-container'
        HOST_PORT = '5000'
        CONTAINER_PORT = '5000'
    }

    stages {
        stage('Checkout Code') {
            steps {
                checkout scm
            }
        }

        stage('Show Workspace') {
            steps {
                sh 'pwd'
                sh 'ls -lah'
            }
        }

        stage('Build Docker Image') {
            steps {
                sh 'docker build -t ${IMAGE_NAME}:latest .'
            }
        }

        stage('Stop Old Container') {
            steps {
                sh '''
                    if [ $(docker ps -aq -f name=${CONTAINER_NAME} | wc -l) -gt 0 ]; then
                      docker rm -f ${CONTAINER_NAME}
                    else
                      echo "No existing container found."
                    fi
                '''
            }
        }

        stage('Run New Container') {
            steps {
                sh 'docker run -d --name ${CONTAINER_NAME} -p ${HOST_PORT}:${CONTAINER_PORT} ${IMAGE_NAME}:latest'
            }
        }

        stage('Verify Container') {
            steps {
                sh 'docker ps | grep ${CONTAINER_NAME}'
                sh 'curl -I http://127.0.0.1:${HOST_PORT} || true'
            }
        }
    }

    post {
        success {
            echo 'Pipeline executed successfully. Application deployed.'
        }
        failure {
            echo 'Pipeline failed. Please check console output.'
        }
    }
}
