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
                // If already running, stop it first
                sh '''
                    docker ps -q --filter "name=myapp" | grep -q . && docker stop myapp && docker rm myapp || true
                    docker run -d --name myapp -p 8080:8080 myapp:latest
                '''
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
