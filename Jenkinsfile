pipeline {
    agent any

    environment {
        DOCKER_IMAGE = "durgesh0923/my-python-app:latest"
    }

    stages {
        stage('Checkout Code') {
            steps {
                checkout([$class: 'GitSCM', branches: [[name: '*/main']], userRemoteConfigs: [[url: 'https://github.com/Durgeshwar-0923/dockermedassign']]])
            }
        }

        stage('Build Docker Image') {
            steps {
                sh "docker build -t ${env.DOCKER_IMAGE} ."
            }
        }

        stage('Login to Docker Hub') {
            steps {
                withDockerRegistry([credentialsId: 'docker-hub-cred', url: 'https://index.docker.io/v1/']) {
                    echo "Successfully authenticated with Docker Hub."
                }
            }
        }

        stage('Push Image to Docker Hub') {
            steps {
                sh "docker push ${env.DOCKER_IMAGE}"
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
