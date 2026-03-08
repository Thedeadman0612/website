pipeline {
    agent any

    stages {
        
        stage('Clone repository') {
            steps {
                git 'https://github.com/Thedeadman0612/website.git'
            }
        }

        stage('Build') {
            steps {
                sh 'docker build -t website:v1 .'
            }
        }

        stage('Push Docker Image') {
            steps {
                sh 'docker tag website:v1 rghadiya/website:v1'
                sh 'docker push rghadiya/website:v1'

            }

        }

        stage('Deploy to kubernetes') {
            steps {
                sh 'kubectl apply -f deployment.yaml'
            }
        }
    }
}
