pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                git 'https://github.com/S-Sasi-dharan/Jenkins-pipeline-demo.git'
            }
        }

        stage('Build') {
            steps {
                echo 'Building the project...'
            }
        }

        stage('Test') {
            steps {
                echo 'Running tests...'
            }
        }
    }

    post {
        success {
            echo 'Build successful!'
        }
        failure {
            echo 'Build failed!'
        }
    }
}
