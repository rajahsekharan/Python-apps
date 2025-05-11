pipeline {
    agent any

    environment {
        // Set the Python virtual environment path
        VENV_PATH = '.venv'
    }

    stages {
        stage('Checkout') {
            steps {
                script {
                    // Checkout the code from Git
                    checkout scm
                }
            }
        }

        stage('Install Dependencies') {
            steps {
                script {
                    // Create a virtual environment if it doesn't exist
                    sh '''
                    if [ ! -d "$VENV_PATH" ]; then
                        python3 -m venv $VENV_PATH
                    fi
                    source $VENV_PATH/bin/activate && pip install -r requirements.txt
                    '''
                }
            }
        }

        stage('Run Tests') {
            steps {
                script {
                    // Run tests (assuming you have a test suite defined)
                    sh 'source $VENV_PATH/bin/activate && pytest'
                }
            }
        }

        stage('Build Docker Image') {
            steps {
                script {
                    // Build Docker image (if applicable)
                    sh 'docker build -t my-python-app .'
                }
            }
        }

        stage('Archive Docker Image') {
            steps {
                script {
                    // Archive Docker image (if applicable)
                    sh 'docker save my-python-app -o my-python-app.tar'
                }
            }
        }
    }

    post {
        always {
            echo 'Pipeline finished.'
        }
        failure {
            echo '❌ Pipeline failed.'
        }
    }
}
