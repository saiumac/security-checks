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


pipeline {
    agent any
    stages {
        stage('Checkout Code') {
            steps {
                git branch: 'main', url: 'https://github.com/saiumac/security-checks', credentialsId: 'github-token'
            }
        }
        stage('Install Dependencies') {
            steps {
                sh 'npm install'  // For installing dependencies (Node.js/React)
            }
        }
        stage('Build Project') {
            steps {
                sh 'npm run build'  // For building the project
            }
        }
        stage('Test') {
            steps {
                sh 'npm test'  // Run tests (if applicable)
            }
        }
        stage('Notify GitHub') {
            steps {
                echo 'Build and tests completed. GitHub workflow will handle deployment to EC2.'
            }
        }
    }
}
