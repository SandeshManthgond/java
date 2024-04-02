pipeline {
    agent any

    stages {
        stage('Build') {
            steps {
                // Build the Java application
                sh 'javac HelloDevOps.java'
            }
        }
        stage('Dockerize') {
            steps {
                // Dockerize the application
                sh 'docker build -t hello-devops .'
            }
        }
        stage('Run') {
            steps {
                // Run the Docker container
                sh 'docker run hello-devops'
            }
        }
        stage('Tag') {
            steps {
                // Tag the Docker image
                sh 'docker tag hello-devops yourdockerhubusername/hello-devops:latest'
            }
        }
        stage('Push') {
            steps {
                // Push the Docker image to Docker Hub
                withCredentials([usernamePassword(credentialsId: 'docker-hub-credentials', passwordVariable: 'DOCKER_PASSWORD', usernameVariable: 'DOCKER_USERNAME')]) {
                    sh 'docker login -u $DOCKER_USERNAME -p $DOCKER_PASSWORD'
                    sh 'docker push yourdockerhubusername/hello-devops:latest'
                }
            }
        }
    }
}
