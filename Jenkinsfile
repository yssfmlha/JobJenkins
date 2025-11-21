pipeline{
	agent any
	tools{
		maven 'M2_HOME'
	}
	environment {
 		APP_ENV = "DEV"
 	 }
	stages {
 		stage('Code Checkout') {
 			steps {
 				git branch: 'master',
 				url: 'https://github.com/hwafa/atelier-jenkins.git',
 				credentialsId: 'jenkins-example-github-pat'
 			}
 		}
 		stage('Code Build') {
 			steps {
 				sh 'mvn test'
 			}
 		}
		stage('Code Package'){
			steps{
				sh'mvn package'
			}
		}
 	}
post {
 always {
 echo "======always======"
 }
 success {
 echo "=====pipeline executed successfully ====="
 }
 failure {
 echo "======pipeline execution failed======"
 }
 }

}