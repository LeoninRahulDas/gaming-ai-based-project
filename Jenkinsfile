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

        stage(docker build)
        {
            steps{
            sh '''
               echo 'building a docker images'
               docker build -t projai:${BUILD_NUMBER} .
               '''
            }
        }
    }
}