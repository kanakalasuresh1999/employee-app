pipeline {
    agent any

    stages {

        stage('Git Checkout') {
            steps {
                git branch: 'main',
                url: 'https://github.com/kanakalasuresh1999/employee-app.git'
            }
        }

        stage('Docker Build') {
            steps {
                sh 'docker build -t suresh4927/employee-app:v1 .'
            }
        }

        stage('Docker Push') {
            steps {
                withCredentials([usernamePassword(
                    credentialsId: 'dockerhub',
                    usernameVariable: 'DOCKER_USER',
                    passwordVariable: 'DOCKER_PASS'
                )]) {

                    sh '''
                    echo $DOCKER_PASS | docker login -u $DOCKER_USER --password-stdin
                    docker push suresh4927/employee-app:v1
                    '''
                }
            }
        }

        stage('Kubernetes Deploy') {
            steps {
                sh 'kubectl rollout restart deployment employee-app'
            }
        }
    }
}
