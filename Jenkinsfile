pipeline {
    agent any

    stages {
        stage('Build Docker Image') {
            steps {
                sh 'docker build -t myapp:latest .'
            }
        }
        stage('Run Container') {
            steps {
                // Stop and remove the old container if it exists
                sh 'docker stop myapp || true'
                sh 'docker rm myapp || true'

                // Run the new container
                sh 'docker run -d --name myapp -p 8080:8080 myapp:latest'
            }
        }
    }

    post {
        success {
            echo '✅ Docker image built and container running!'
        }
        failure {
            echo '❌ Something went wrong with the Docker pipeline.'
        }
    }
}
