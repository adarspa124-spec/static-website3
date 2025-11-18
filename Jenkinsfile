pipeline {
    agent any

    stages {

        stage('Checkout Code') {
            steps {
                echo "Pulling latest website code..."
                checkout scm
            }
        }

        stage('Build Docker Image') {
            steps {
                echo "Building NGINX Docker image..."
                bat 'docker build -t static-site:1 .'
            }
        }

        stage('Stop Old Container') {
            steps {
                echo "Stopping old container if running..."
                bat '''
                docker stop static_container || exit 0
                docker rm static_container || exit 0
                '''
            }
        }

        stage('Run New Container') {
            steps {
                echo "Running new NGINX container..."
                bat 'docker run -d -p 80:80 --name static_container static-site:1'
            }
        }
    }
}
