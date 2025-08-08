pipeline {
    agent any

    environment {
        IMAGE_NAME = "localweb"
        CONTAINER_NAME = "mywebcontainer"
        HOST_PORT = "8082"
        CONTAINER_PORT = "80"
        GIT_REPO = "https://github.com/mishashah1/docker-web-project.git"
    }

    stages {
        stage('Clone Repository') {
            steps {
                git branch: 'main', url: "${GIT_REPO}"
            }
        }

        stage('Build Docker Image') {
            steps {
                script {
                    sh """
                        echo 'Building Docker image locally...'
                        docker build -t ${IMAGE_NAME}:latest .
                    """
                }
            }
        }

        stage('Stop and Remove Old Container') {
            steps {
                script {
                    sh """
                        echo 'Stopping old container if exists...'
                        docker stop ${CONTAINER_NAME} || true
                        docker rm ${CONTAINER_NAME} || true
                    """
                }
            }
        }

        stage('Run New Container') {
            steps {
                script {
                    sh """
                        echo 'Starting new container on port ${HOST_PORT}...'
                        docker run -d --name ${CONTAINER_NAME} -p ${HOST_PORT}:${CONTAINER_PORT} ${IMAGE_NAME}:latest
                    """
                }
            }
        }

        stage('Verify Container') {
            steps {
                script {
                    sh "docker ps"
                    echo "Access your app at: http://<server-ip>:${HOST_PORT}"
                }
            }
        }
    }
}
