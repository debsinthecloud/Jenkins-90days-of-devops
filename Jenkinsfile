pipeline {
    agent any

    stages {
        stage('Declarative: Checkout SCM') {
            steps {
                checkout scm
            }
        }
        stage('Build Docker Image') {
            steps {
                sh 'docker build -t myapp:latest .'
            }
        }
        stage('Run Container') {
            steps {
                sh 'docker stop myapp || true' // Use '|| true' to prevent failure if container doesn't exist
                sh 'docker rm myapp || true'
                sh 'docker run -d --name myapp -p 8082:8080 myapp:latest'
            }
        }
        stage('Declarative: Post Actions') {
            steps {
                echo "✅ Pipeline completed successfully. Your app is now running on port 8082."
            }
        }
    }
}

