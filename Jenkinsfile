pipeline {
    agent any
    tools {
    	maven 'local_maven'
    }
    stages{
        stage('Build'){
            steps {
                bat 'mvn clean package'
            }
            post {
                success {
                    echo 'starting archiving ...'
                    archiveArtifacts artifacts: '**/target/*.war'
                }
            }
        }
        stage('Deploy to stage (localhost:8081)'){
        	steps{
        		build job: 'deploy-course-maven-project-for-pipeline' 
        	}
        }
    }
}