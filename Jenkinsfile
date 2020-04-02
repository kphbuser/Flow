pipeline {
	agent any
	tools {
		maven 'apache-maven'
		// jdk 'java-8'
	}
	stages {
		stage('git-code-checkout'){
			steps {
				git "https://github.com/kphbuser/Flow.git"
			}
		}
		stage('mavne-build'){
			steps {
				sh 'mvn clean package -DskipTests'
				}
			}
		stage('Artifact_upload'){
				steps{
					withCredentials([usernmeColonPassword(credentialsId: 'nexus-username-password', variable: 'USERNAME_PASSWORD')]) {
						sh 'curl -v --fail --user $USERNAME_PASSWORD --upload-file ./target/*.war http://13.232.1.88:8081/nexus/content/repositories/tomcat/'
					}
				}
			}
		}
}