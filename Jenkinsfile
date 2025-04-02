pipeline{
    agent any
    stages{
            stage('Unit Test'){
                steps{
                sh "echo Running unittest"
            }
        }
           stage('Build Stage'){
                steps{
                sh "echo Building application"
            }
        }
           stage('Package application'){
                steps{
                sh "echo Packaging application"
            }
        }
           stage('Deploy app'){
                steps{
                sh "echo Deploying the app"
            }
        }
    }
}