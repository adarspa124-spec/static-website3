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
                echo "Building Docker image..."
                sh 'docker build -t myapp:latest .'
            }
        }

        stage('Deploy') {
            steps {
                echo "Deploying the project..."
                sh 'docker run -d -p 8080:8080 myapp:latest'
            }
        }
    }
}
