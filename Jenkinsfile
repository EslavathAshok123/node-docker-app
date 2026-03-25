pipeline {
    agent any

    stages {

        stage('Checkout from GitHub') {
            steps {
                git branch: 'main',
                    url: 'https://github.com/EslavathAshok123/node-docker-app.git'
            }
        }

        stage('Install Dependencies') {
            steps {
                sh 'npm install'
            }
        }

        stage('Build Docker Image') {
            steps {
                sh """
                docker build -t node-docker-app:${BUILD_NUMBER} .
                docker tag node-docker-app:${BUILD_NUMBER} EslavathAshok123/node-docker-app:${BUILD_NUMBER}
                """
            }
        }

        stage('Push Docker Image') {
            steps {
                sh "docker push EslavathAshok123/node-docker-app:${BUILD_NUMBER}"
            }
        }
        
        stage('Create container') {
            steps {
                sh "docker run -d -p 3000:8000 EslavathAshok123/node-docker-app:${BUILD_NUMBER}"
            }
        }

    }
}
