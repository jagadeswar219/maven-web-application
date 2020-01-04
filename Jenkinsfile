// Powered by Infostretch 

timestamps {

node () {

	stage ('free1 - Checkout') {
 	 checkout([$class: 'GitSCM', branches: [[name: '*/master']], doGenerateSubmoduleConfigurations: false, extensions: [], submoduleCfg: [], userRemoteConfigs: [[credentialsId: 'GIT_credentials', url: 'https://github.com/jagadeswar219/maven-web-application.git']]]) 
	}
	stage ('free1 - Build') {
 			// Maven build step
	withMaven(maven: 'maven-3.6.3') { 
 			if(isUnix()) {
 				sh "mvn clean install sonar:sonar deploy " 
			} else { 
 				bat "mvn clean install sonar:sonar deploy " 
			} 
 		} 
	}
}
}