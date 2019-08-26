pipeline {
    agent any
    tools{
        maven 'local_maven'
    }

    stages{
        stage('Build'){
            steps {
                bat 'mvn clean package'
            }
            post {
                success {
                    echo 'starting archiving now'
                    archiveArtifacts artifacts: '**/target/*.war'
                }
            }
        }
        stage('Deploy to staging'){
            steps{
                build job:'deploy-course-maven-project-for-pipeline'
            }
        }

        stage ('Deploy to Production'){
            steps{
                timeout(time:5, unit:'DAYS'){
                    input message:'should war be deployed to prod environment ?' 
                }

                build job: 'deploy-course-maven-project-to-prod-for-pipeline'
            }
            post {
                success {
                    echo 'successfully deployed to prod environment'
                }

                failure {
                    echo 'failed to deploy to prod'
                }
            }
        } 
    }
}