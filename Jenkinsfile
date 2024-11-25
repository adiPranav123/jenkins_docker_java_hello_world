pipeline {
    agent any
    environment {
        DOCKER_IMAGE = 'hello-world-java:latest'  // Docker image name
    }

    stages {
        stage('Checkout') {
            steps {
                // Checkout the source code from the repository
                checkout scm
            }
        }
        stage('Build') {
            steps {
                // Compile the Java program (assuming HelloWorld.java is in the repository)
                sh 'javac HelloWorld.java'
            }
        }
        stage('Package') {
            steps {
                // Package the compiled class into a JAR file
                sh 'jar cf HelloWorld.jar HelloWorld.class'
            }
        }
        stage('Docker Build') {
            steps {
                // Build the Docker image using the Dockerfile in the repository
                sh """
                docker build -t $DOCKER_IMAGE .
                """
            }
        }
    }

    post {
        success {
            // Print a message on successful build
            echo 'Build completed successfully.'
        }
        failure {
            // Print a message on failed build
            echo 'Build failed.'
        }
    }
}
