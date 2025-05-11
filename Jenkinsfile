pipeline {
    agent any

    environment {
        IMAGE_NAME = "my-python-app"
    }

    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }

        stage('Install Dependencies') {
            steps {
                sh 'pip install -r requirements.txt'
            }
        }

        stage('Run Tests') {
            steps {
                sh 'pytest tests/'
            }
        }

        stage('Build Docker Image') {
            steps {
                sh "docker build -t $IMAGE_NAME ."
            }
        }

        stage('Archive Docker Image') {
            steps {
                sh "docker save $IMAGE_NAME > ${IMAGE_NAME}.tar"
                archiveArtifacts artifacts: "${IMAGE_NAME}.tar", fingerprint: true
            }
        }
    }

    post {
        success {
            echo '✅ Pipeline succeeded.'
        }
        failure {
            echo '❌ Pipeline failed.'
        }
    }
}
