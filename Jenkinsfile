pipeline {
    agent any

    environment {
        IMAGE_NAME = "flask-demo"
    }

    stages {
        stage('Checkout') {
            steps {
                git 'https://github.com/harjeetmehra22-png/ci-cd-demo.git'
            }
        }

        stage('Build Docker Image') {
            steps {
                script {
                    sh 'docker build -t $IMAGE_NAME .'
                }
            }
        }

        stage('Run Container') {
            steps {
                script {
                    sh 'docker run -d -p 5000:5000 --name flask-demo $IMAGE_NAME'
                }
            }
        }

        stage('Test') {
            steps {
                script {
                    sh 'sleep 5 && curl -f http://localhost:5000'
                }
            }
        }

        stage('Cleanup') {
            steps {
                script {
                    sh 'docker stop flask-demo || true && docker rm flask-demo || true'
                }
            }
        }
    }

    post {
        always {
            echo "Cleaning up workspace..."
            deleteDir()
        }
    }
}
