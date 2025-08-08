pipeline {
    agent any

    stages {
        stage('Clone Repository') {
            steps {
                git 'https://github.com/mishashah1/docker-web-project.git'
            }
        }

        stage('Build Docker Image') {
            steps {
                sh 'docker build -t mywebimage .'
            }
        }

        stage('Run Docker Container') {
            steps {
                sh 'docker run -d -p 8085:80 --name webcontainer mywebimage || echo "Container already running"'
            }
        }
    }
}
