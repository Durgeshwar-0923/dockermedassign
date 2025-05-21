pipeline {
    agent any

    stages {
        stage('Checkout Code') {
            steps {
                git 'https://github.com/Durgeshwar-0923/dockermedassign.git'
            }
        }

        stage('Build Docker Image') {
            steps {
                sh 'docker build -t durgesh0923/minfyassign:latest .'
            }
        }

        stage('Login to Docker Hub') {
            steps {
                withDockerRegistry([credentialsId: 'docker-hub-cred', url: 'https://index.docker.io/v1/']) {
                    echo 'Successfully authenticated with Docker Hub.'
                }
            }
        }

        stage('Push Image to Docker Hub') {
            steps {
                sh 'docker push durgesh0923/minfyassign:latest'
            }
        }
    }

    post {
        failure {
            echo 'Pipeline failed! Check logs for errors.'
        }
    }
}
