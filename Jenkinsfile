pipeline{
    agent any
     environment {
        dockerImage = "mesworup/devops-evening"  
    }
    stages{
            stage('Build Java App'){
                steps{
                sh ' mvn -f pom.xml clean package'
            }
            post{
                success {
                    echo "Build Completed, so archieving the war file"
                archiveArtifacts artifacts: '**/*.war', followSymlinks: false
                }
            }
        }
           stage('Create Docker Image'){
                steps{
                    copyArtifacts filter: '**/*.war', fingerprintArtifacts: true, projectName: env.JOB_NAME, selector: specific(env.BUILD_NUMBER)
                    echo "Creating Docker Image"
                    sh 'whoami'
                    sh 'docker build -t $dockerImage:$BUILD_NUMBER .'
            }
        }
           stage('Tag and Push image'){
                steps{
                withDockerRegistry([credentialsId: 'dockerhub-credentials', url: '']) {
                    sh '''
                    docker push $dockerImage:$BUILD_NUMBER
                    '''
            }
        }
           stage('Deploy app'){
                steps{
                
                }
            }
        }
    }
}