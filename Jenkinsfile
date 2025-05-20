pipeline {
    agent any

    environment {
        DOCKER_IMAGE = "docker0923/my-python-app:latest"
    }

    stages {
        stage('Checkout Code') {
            steps {
                git branch: 'main', url: 'https://github.com/Durgeshwar-0923/dockermedassign'
            }
        }

        stage('Build Docker Image') {
            steps {
                sh '''
                    docker build -t $DOCKER_IMAGE .
                '''
            }
        }

        stage('Login to Docker Hub') {
            steps {
                withDockerRegistry([credentialsId: 'docker-hub-cred', url: 'https://index.docker.io/v1/']) {
                    sh 'docker login'
                }
            }
        }

        stage('Push Image to Docker Hub') {
            steps {
                sh '''
                    docker push $DOCKER_IMAGE
                '''
            }
        }

        stage('Cleanup') {
            steps {
                sh 'docker system prune -f'
            }
        }
    }

    post {
        success {
            echo "Docker image successfully pushed to Docker Hub!"
        }
        failure {
            echo "Pipeline failed! Check logs for errors."
        }
    }
}
