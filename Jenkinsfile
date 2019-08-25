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
    }
}