pipeline {
    agent any

    environment {
        IMAGE_NAME = "flask-app"
        CONTAINER_NAME = "flask-container"
        APP_PORT = "8080"
    }

    stages {
        stage('Clone Code') {
            steps {
                git 'https://github.com/sandeepbikkana/CICD-Jenkins-web.git'  // Replace with your repo
            }
        }

        stage('Build Docker Image') {
            steps {
                sh "docker build -t ${IMAGE_NAME} ."
            }
        }

        stage('Test') {
            steps {
                sh "docker run --rm ${IMAGE_NAME} python -c 'import flask; print(\"Flask is working\")'"
            }
        }

        stage('Deploy') {
            steps {
                sh "docker rm -f ${CONTAINER_NAME} || true"
                sh "docker run -d -p ${APP_PORT}:${APP_PORT} --name ${CONTAINER_NAME} ${IMAGE_NAME}"
            }
        }
    }

    post {
        success {
            echo " App deployed successfully at http://<jenkins-ip>:${APP_PORT}"
        }
        failure {
            echo " Build failed"
        }
    }
}

