pipeline {
    agent any
    
    stages {
        
        stage('Checkout Repository') {
            steps {
                git branch: 'main', url: 'https://github.com/mishashah1/docker-web-project.git'
            }
        }
        
        stage('Build Docker Image') {
            steps {
                sh 'docker build -t mywebimage .'
            }
        }
        
        stage('Run Container') {
            steps {
                sh 'docker run -d -p 8080:80 --name mywebcontainer mywebimage'
            }
        }
        
    }
    
    post {
        always {
            sh 'docker ps -a'
        }
        cleanup {
            sh 'docker stop mywebcontainer || true'
            sh 'docker rm mywebcontainer || true'
        }
    }
}
