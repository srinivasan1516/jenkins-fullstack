pipeline {

    agent any

    tools {
        nodejs "node18"
    }

    environment {
        FRONTEND_DIR = "frontend"
        BACKEND_DIR = "backend"
    }

    stages {

        stage('Clone Code') {
            steps {
                git branch: 'main',
                url: 'https://github.com/srinivasan1516/jenkins-fullstack.git'
            }
        }

        stage('Install Frontend Dependencies') {
            steps {
                dir("${FRONTEND_DIR}") {
                    sh 'npm install'
                }
            }
        }

        stage('Build Frontend') {
            steps {
                dir("${FRONTEND_DIR}") {
                    sh 'npm run build'
                }
            }
        }

        stage('Deploy Frontend') {
            steps {
                sh '''
                sudo rm -rf /var/www/html/*
                sudo cp -r frontend/build/* /var/www/html/
                '''
            }
        }

        stage('Install Backend Dependencies') {
            steps {
                dir("${BACKEND_DIR}") {
                    sh 'npm install'
                }
            }
        }

        stage('Start Backend') {
            steps {
                dir("${BACKEND_DIR}") {
                    sh '''
                    pm2 delete backend-app || true
                    pm2 start server.js --name backend-app
                    pm2 save
                    '''
                }
            }
        }

    }

}
