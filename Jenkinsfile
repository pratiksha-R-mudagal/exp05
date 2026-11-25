pipeline {
    agent any

    environment {
        DOCKER_IMAGE = 'your-dockerhub-username/jenkins-demo'
        DOCKER_CREDENTIALS = 'dockerhub_credentials'
    }

    stages {

        stage('Checkout') {
            steps {
                git branch: 'main',
                    url: 'https://github.com/pratiksha-R-mudagal/exp05.git'
            }
        }

        stage('Build Application') {
            steps {
                echo 'Building the application...'
                bat 'dir'
            }
        }

        stage('Build Docker Image') {
            steps {
                bat 'pratikshamudagl/exp5'
            }
        }

        stage('Push Docker Image') {
            steps {
                withCredentials([
                    usernamePassword(
                        credentialsId: 'dockerhub_credentials',
                        usernameVariable: 'DOCKER_USER',
                        passwordVariable: 'DOCKER_PASS'
                    )
                ]) {
                    bat 'docker login -u %DOCKER_USER% -p %DOCKER_PASS%'
                    bat 'docker push %DOCKER_IMAGE%:latest'
                    bat 'docker logout'
                }
            }
        }
    }

    post {
        success {
            echo 'Pipeline executed successfully!'
        }

        failure {
            echo 'Pipeline execution failed!'
        }
    }
}
