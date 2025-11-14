pipeline {
    agent any

    environment {
        DOCKERHUB_CRED = 'dockerhub'
        DOCKERHUB_REPO = 'moatta22/hellpapp'
    }

    stages {

        stage('Checkout') {
            steps {
                checkout scm
            }
        }

        stage('Build Docker Image') {
            steps {
                script {
                    sh """
                    docker build -t ${DOCKERHUB_REPO}:latest .
                    """
                }
            }
        }

        stage('Login to Docker Hub') {
            steps {
                script {
                    withCredentials([usernamePassword(credentialsId: DOCKERHUB_CRED,
                                                     usernameVariable: 'moatta22',
                                                     passwordVariable: 'Welcome1EG@ad#95')]) {
                        sh "echo $DOCKER_PASS | docker login -u $DOCKER_USER --password-stdin"
                    }
                }
            }
        }

        stage('Push Image') {
            steps {
                script {
                    sh "docker push ${DOCKERHUB_REPO}:latest"
                }
            }
        }
    }

    post {
        always {
            sh "docker logout || true"
        }
    }
}

