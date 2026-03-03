pipeline {
    agent any

    stages {

        stage('Build') {
            steps {
                sh 'docker build -t abode-webapp .'
            }
        }

        stage('Test') {
            steps {
                sh 'echo Running tests'
            }
        }

        stage('Deploy to Prod') {
            when {
                branch 'master'
            }
            steps {
                sh '''
                docker stop web || true
                docker rm web || true
                docker run -d -p 80:80 --name web abode-webapp
                '''
            }
        }
    }
}
