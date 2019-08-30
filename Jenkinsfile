pipeline {
    agent any
    
    tools{
        maven 'local_maven'
    } 
    
    parameters { 
             string(name: 'tomcat_dev', defaultValue: '18.222.30.118', description: 'Staging Server') 
             string(name: 'tomcat_prod', defaultValue: '3.14.5.101', description: 'Production Server') 
    } 
    
    triggers { 
             pollSCM('* * * * *') // Polling Source Control 
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
        
        stage('Deployment to AWS Stage and Prod'){ 
                parallel{
	                    stage ('Deploy to Staging'){
	                        steps { 
	                            bat "pscp -i C:/Users/dings/Desktop/tmp-aws-for-jenkins/tomcat-demo.pem.txt **/target/*.war ec2-user@${params.tomcat_dev}:/var/lib/tomcat8/webapps" 
	                        } 
	                    } 
	                    stage ("Deploy to Production"){ 
	                        steps { 
	                            bat "pscp -i C:/Users/dings/Desktop/tmp-aws-for-jenkins/tomcat-demo.pem.txt **/target/*.war ec2-user@${params.tomcat_prod}:/var/lib/tomcat8/webapps" 
	                        } 
	                    }

                }
        }
 
    }
}
