pipeline{
	agent any
	tools{
		maven 'M2_HOME'
	}
	environment {
 		DOCKER_CREDENTIALS=credentials('docker-hub-creds')
 	 }
	stages {
 		stage('Code Checkout') {
 			steps {
 				git branch: 'main',
 				url: 'https://github.com/yssfmlha/Mlaouhia_Youssef_4SAE9.git'
 			}
 		}
 		stage('Code Build') {
 			steps {
 				sh 'mvn test'
 			}
 		}
		stage('Code Package'){
			steps{
				sh 'mvn package'
			}
		}
		stage('Docker Build'){
			steps{
				script{
					sh "docker build -t yssfmlha/student-management:1.0 ."
				}
			}
		}
		stage('Docker Push'){
			steps{
				script{
					sh 'echo $DOCKER_CREDENTIALS_PSW | docker login -u $DOCKER_CREDENTIALS_USR --password-stdin'
					sh "docker push yssfmlha/student-management:1.0"
				}
			}
		}
		stage('Kubernetes Deployment'){
			steps{
				script{
					sh "kubectl apply -f k8s/spring-deployment.yaml -n devops"
					sh "kubectl apply -f k8s/mysql-deployment.yaml -n devops"
					sh "kubectl rollout status deployment/spring-app -n devops"
				}
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
