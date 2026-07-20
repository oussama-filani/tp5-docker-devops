pipeline {
    agent any

    environment {
        registry = "filani07/jenkins"
        registryCredential = "8b2e7c91-5d4a-4f38-9b1f-c6d2e9a7f154"
    }

    stages {
        stage('Building Image') {
            steps {
                bat "docker build -t ${registry}:${BUILD_NUMBER} ."
            }
        }

        stage('Publish Image') {
            steps {
                script {
                    withCredentials([usernamePassword(
                        credentialsId: "${registryCredential}",
                        passwordVariable: 'DOCKER_PWD',
                        usernameVariable: 'DOCKER_USER'
                    )]) {
                        // Switch to default context to be safe on Windows
                        bat "docker context use default"

                        // Login to Docker Hub using Jenkins credentials
                        bat "echo %DOCKER_PWD% | docker login -u %DOCKER_USER% --password-stdin"

                        // Push the Docker image
                        bat "docker push ${registry}:${BUILD_NUMBER}"
                    }
                }
            }
        }
    }
}