pipeline {
    agent any
    stages {
        stage('Checkout') {
            steps {
                git branch: 'main', url: 'https://github.com/saiumac/security-checks.git'
            }
        }
        stage('Install Dependencies') {
            steps {
                sh 'npm install'
            }
        }
        stage('Build App') {
            steps {
                sh 'npm run build'
            }
        }
        stage('Deploy to EC2') {
            steps {
                sshagent(['your-ssh-credentials-id']) {
                    sh '''
                    ssh -o StrictHostKeyChecking=no ec2-user@54.221.44.26 '
                    sudo chown -R ec2-user:ec2-user /home/ec2-user/security-checks && \
                    git pull origin main && \
                    npm install && \
                    npm run build && \
                    sudo npm install -g pm2 serve && \
                    pm2 stop all || true && \
                    pm2 start \'serve -s build -l 3000\' --name restaurant-app
                    '
                    '''
                }
            }
        }
    }
}
