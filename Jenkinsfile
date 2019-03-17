pipeline {
    agent {
    node {
        label 'centOs-Slave'
  	  }
	}
    environment {
        branch = 'master'
        scmUrl = 'https://github.com/iamrameshtk/SampleApp.git'
        serverPort = '8080'
    }
    stages {
        stage('checkout git') {
             steps {
             git branch: branch, credentialsId: 'GitCredentials', url: scmUrl
                  }
			}
        stage('build') {
              steps {
		      sh 'mvn clean package -DskipTests=true,-DnewVersion='${env.BUILD_NUMBER}'
                    }
			}
		}	
post {
    	success {
		echo 'Sending Success Notification'	
		mail to: 'rameshkasinath08@gmail.com', subject: 'Pipeline Success', body: "${env.BUILD_URL}"
           	 }
	failure {
		echo 'Sending failure Notification'	
		mail to: 'rameshkasinath08@gmail.com', subject: 'Pipeline failed', body: "${env.BUILD_URL}"
            }
     }
}
