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
                docker tag node-docker-app:${BUILD_NUMBER} ashok918/node-docker-app:${BUILD_NUMBER}
                """
            }
        }

        stage('Login to DockerHub') {
            steps {
                withCredentials([usernamePassword(credentialsId: 'dockerhub-creds', usernameVariable: 'USER', passwordVariable: 'PASS')]) {
                    sh 'echo $PASS | docker login -u $USER --password-stdin'
                }
            }
        }
        stage('Push Docker Image') {
            steps {
                sh "docker push ashok918/node-docker-app:${BUILD_NUMBER}"
            }
        }
        
        stage('Create container') {
            steps {
                sh "docker run -d -p 3001:8000 ashok918/node-docker-app:${BUILD_NUMBER}"
            }
        }

    }
}
