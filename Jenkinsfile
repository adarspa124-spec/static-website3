pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                echo 'Pulling website code...'
                git branch: 'main', url: 'https://github.com/shivnathyadav73/static-website.git'
            }
        }

        stage('Build Docker Image') {
            steps {
                powershell """
                    docker build -t static-website:latest .
                """
            }
        }

        stage('Run Container') {
            steps {
                powershell """
                    docker stop static-web -ErrorAction SilentlyContinue
                    docker rm static-web -ErrorAction SilentlyContinue
                    docker run -d --name static-web -p 8080:80 static-website:latest
                """
            }
        }
    }

    post {
        success {
            echo "Website running at: http://localhost:8080"
        }
    }
}
