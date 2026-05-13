pipeline
{
    agent any

    tools{
        maven 'maven'
        jdk 'java'
    }

    stages{

        stage('git-checkout')
        {
            steps{
                git url: 'https://github.com/LeoninRahulDas/gaming-ai-based-project.git',
                branch : 'master'
            }
        }

        stage('compile')
        {
            steps{
                sh '''
                   echo 'compiling the code'
                   mvn compile
                '''
            }
        }

        stage('build')
        {
            steps{
                sh '''
                   echo 'Build the code'
                   mvn package
                  '''
            }
        }

        stage('docker build')
        {
            steps{
                sh """
                    echo 'Building a docker image'
                    docker build -t myapp:${BUILD_NUMBER}
                   """
            }
        }
    }
}