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
		stage('Release'){
			when {
				branch 'master'
			}
			steps{
					withCredentials([usernameColonPassword(credentialsId: 'nexus_username_password', variable: 'USERNAME_PASSWORD')]) {
						sh 'curl -v --fail --user $USERNAME_PASSWORD --upload-file ./target/*.war http://3.6.38.29:8081/nexus/content/repositories/tomcat/'
					}
				}
			}
		stage('snapshot'){
			when {
				not {
					branch 'master'
				}
			steps{
					withCredentials([usernameColonPassword(credentialsId: 'nexus_username_password', variable: 'USERNAME_PASSWORD')]) {
						sh 'curl -v --fail --user $USERNAME_PASSWORD --upload-file ./target/*.war http://3.6.38.29:8081/nexus/content/repositories/snapshot/'
					}
				}
			}
		}
	}
}
