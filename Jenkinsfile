pipeline {
    agent any

    stages {

        stage('Test') {
            steps {
                echo "Running basic tests..."
            }
        }

        stage('Build') {
            steps {
                echo "Building the project..."
            }
        }

        stage('Docker Build') {
            steps {
                echo "Building Docker image on Windows..."
                bat 'docker build -t sw-lab:11 .'
            }
        }

        stage('Deploy') {
            steps {
                echo "Running Docker container on Windows..."
                bat 'docker run -d -p 8080:8080 --name myapp_container myapp:latest'
            }
        }
    }
}
