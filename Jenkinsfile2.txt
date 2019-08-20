pipeline {
    agent any
    stages{
        stage('Build'){
            steps {
                sh 'mvn clean package'
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