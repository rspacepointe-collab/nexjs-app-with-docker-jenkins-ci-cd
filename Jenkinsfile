pipeline {
    agent any

    environment {
        APP_NAME = "nextjs-app"
        PORT = "3000"
    }

    stages {
        stage('Checkout Code') {
            steps {
                git branch: 'dev',
                url: 'https://github.com/rspacepointe-collab/nexjs-app-with-docker-jenkins-ci-cd.git'
            }
        }

        stage('Build Docker Image') {
            steps {
                sh 'docker build -t $APP_NAME .'
            }
        }

        stage('Stop Old Container') {
            steps {
                sh '''
                docker stop $APP_NAME || true
                docker rm $APP_NAME || true
                '''
            }
        }

        stage('Run Container') {
            steps {
                sh '''
                docker run -d \
                --name $APP_NAME \
                -p 3000:3000 \
                $APP_NAME
                '''
            }
        }
    }
}
