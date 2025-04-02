pipeline{
    agent any
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
                    sh 'docker build -t localtomcatimg:$BUILD_NUMBER .'
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