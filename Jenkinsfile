pipeline {
    agent any

    stages {

        stage('Build') {
            steps {
                sh 'docker build -t website:v1 .'
            }
        }

        stage('Push Docker Image') {
            steps {
                withCredentials([usernamePassword(credentialsId: 'dockerhub-creds', usernameVariable: 'USER', passwordVariable: 'PASS')]) {
                    sh '''
                    echo $PASS | docker login -u $USER --password-stdin
                    docker tag website:v1 rghadiya/website:v1
                    docker push rghadiya/website:v1
                    '''
                }
            }
        }

        stage('Deploy to kubernetes') {
            steps {
               sh '''
               export KUBECONFIG=/var/jenkins_home/.kube/config
               kubectl get nodes
               kubectl apply -f deployment.yaml
               kubectl apply -f service.yaml
               '''
            }
       }
    }
}
