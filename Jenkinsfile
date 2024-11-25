pipeline {
    agent any
    environment {
        DOCKER_IMAGE = 'blackopsgun/jenkins-python-88:1.0'  // Correct Docker image name
    }

    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }
        stage('Build') {
            steps {
                sh 'javac HelloWorld.java'
            }
        }
        stage('Package') {
            steps {
                sh 'jar cf HelloWorld.jar HelloWorld.class'
            }
        }
        stage('Docker Build') {
            steps {
                sh 'docker build -t $DOCKER_IMAGE .'
            }
        }
        stage('Push to DockerHub') {
            steps {
                withCredentials([usernamePassword(credentialsId: 'adipra', usernameVariable: 'DOCKER_USERNAME', passwordVariable: 'DOCKER_PASSWORD')]) {
                    script {
                        // Log into Docker Hub
                        sh 'echo $DOCKER_PASSWORD | docker login -u $DOCKER_USERNAME --password-stdin'

                        // Push the Docker image to Docker Hub
                        sh 'docker push $DOCKER_IMAGE'
                    }
                }
            }
        }
    }
    post {
        success {
            echo 'Build completed successfully.'
        }
        failure {
            echo 'Build failed.'
        }
    }
}
                                                
