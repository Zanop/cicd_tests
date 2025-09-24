pipeline {
    agent any   // Run on any available Jenkins agent

    environment {
        APP_NAME = "CICD Test"
    }

    stages {
        stage('Checkout') {
            steps {
                // Pull code from Git
                git branch: 'main', url: 'git@github.com:Zanop/cicd_tests.git'
            }
        }

        stage('Build') {
            steps {
                echo "Building ${APP_NAME}..."
                python3 -m py_compile main.py
            }
        }

        stage('Test') {
            steps {
                echo "Running tests..."
                main.py
            }
        }

        stage('Package') {
            steps {
                echo "Packaging artifact..."
                sh 'docker build -t myapp:latest .'
            }
        }

        stage('Deploy') {
            steps {
                echo "Deploying application..."
                mkdir build
                cp main.py build/
            }
        }
    }

    post {
        success {
            echo "Pipeline finished successfully!"
        }
        failure {
            echo "Pipeline failed. Please check logs."
        }
    }
}


