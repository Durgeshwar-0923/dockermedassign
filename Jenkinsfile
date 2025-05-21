pipeline {
    agent any

    environment {
        DOCKER_IMAGE = 'durgesh0923/myapp:latest'
    }

    stages {
        stage('Clone Repository') {
            steps {
                git 'https://github.com/Durgeshwar-0923/dockermedassign.git'
            }
        }

        stage('Build Docker Image') {
            steps {
                sh 'docker build -t myapp .'
            }
        }

        stage('Push to Docker Hub') {
            steps {
                withDockerRegistry([credentialsId: 'docker-hub-cred', url: 'https://index.docker.io/v1/']) {
                    sh "docker tag myapp $DOCKER_IMAGE"
                    sh "docker push $DOCKER_IMAGE"
                }
            }
        }

        stage('Deploy Container') {
            steps {
                sh "docker run -d -p 8081:8081 $DOCKER_IMAGE"
            }
        }
    }
}
