pipeline {
    agent any

    stages {

        stage('Checkout') {
            steps {
                echo "Checking out code..."
                checkout scm
            }
        }

        stage('Clean old containers') {
            steps {
                echo "Cleaning old Docker containers..."
                bat '''
                docker stop local-app || exit 0
                docker rm local-app || exit 0
                '''
            }
        }

        stage('Build Image') {
            steps {
                echo "Building Docker image..."
                bat '''
                docker build -t local-app .
                '''
            }
        }

        stage('Run Container') {
            steps {
                echo "Starting container..."
                bat '''
                docker run -d -p 3000:3000 --name local-app local-app
                '''
            }
        }
    }

    post {
        success {
            echo "🚀 Pipeline completed successfully!"
        }
        failure {
            echo "❌ Pipeline failed — check the logs."
        }
    }
}
