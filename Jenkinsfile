pipeline {
    agent any

    environment {
        DOCKERHUB_CREDENTIALS = 'dockerhub'     // Jenkins me create kiya hua secret ID
        DOCKER_IMAGE = "root465/static-website:latest"
    }

    stages {

        stage('Checkout') {
            steps {
                git branch: 'main',
                    url: 'https://github.com/adarspa124-spec/static-website3.git'
            }
        }

        stage('Build Docker Image') {
            steps {
                sh 'docker build -t $DOCKER_IMAGE .'
            }
        }

        stage('Push to DockerHub') {
            steps {
                withCredentials([usernamePassword(
                    credentialsId: DOCKERHUB_CREDENTIALS,
                    usernameVariable: 'USERNAME',
                    passwordVariable: 'PASSWORD'
                )]) {
                    sh """
                        echo "$PASSWORD" | docker login -u "$USERNAME" --password-stdin
                        docker push $DOCKER_IMAGE
                    """
                }
            }
        }

        stage('Deploy to Kubernetes') {
            steps {
                sh """
                    kubectl apply -f k8deployment.yaml
                """
            }
        }
    }

    post {
        success {
            echo "Deployment complete! Visit: http://<server-ip>:30090"
        }
    }
}
