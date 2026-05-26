pipeline {

    agent any

    stages {

        stage('Clone Code') {
            steps {
                git branch: 'main',
                url: 'https://github.com/srinivasan1516/jenkins-fullstack.git'
            }
        }

        stage('Install Dependencies') {
            steps {
                sh 'npm install'
            }
        }

        stage('Build') {
            steps {
                sh 'npm run build'
            }
        }

        stage('Start Application') {
            steps {
                sh '''
                pm2 delete app || true
                pm2 start npm --name app -- start
                '''
            }
        }
    }
}
