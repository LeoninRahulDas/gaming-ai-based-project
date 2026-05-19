pipeline {
    agent any

    tools {
        maven 'maven'
        jdk 'java'
    }

    environment {
        IMAGE_NAME = "leorahuldas/devsecops:${GIT_COMMIT}"
    }

    stages {

        stage('git-checkout') {
            steps {
                git url: 'https://github.com/LeoninRahulDas/gaming-ai-based-project.git',
                    branch: 'master'
            }
        }

        stage('compile') {
            steps {
                sh '''
                    echo 'Compiling the code'
                    mvn compile
                '''
            }
        }

        stage('build') {
            steps {
                sh '''
                    echo 'Building the code'
                    mvn package
                '''
            }
        }

        stage('docker build') {
            steps {
                sh """
                    echo 'Building Docker image'
                    docker build -t ${IMAGE_NAME} .
                """
            }
        }

        stage('docker login') {
            steps {
                script {
                    withCredentials([
                        usernamePassword(
                            credentialsId: 'dockerhub-creds',
                            passwordVariable: 'DOCKER_PASSWORD',
                            usernameVariable: 'DOCKER_USERNAME'
                        )
                    ]) {

                        sh '''
                            echo 'Docker login'
                            echo $DOCKER_PASSWORD | docker login -u $DOCKER_USERNAME --password-stdin
                        '''
                    }
                }
            }
        }

        stage('docker push') {
            steps {
                sh """
                    echo 'Pushing Docker image'
                    docker push ${IMAGE_NAME}
                """
            }
        }
    }
}