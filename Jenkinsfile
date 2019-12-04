node{
//node('master'){

  //http://JenkinsServerIPAddress:8080/pipeline-syntax/globals#currentBuild
  //Getting the  env  global varibale values

  echo "GitHub BranhName ${env.BRANCH_NAME}"
  echo "Jenkins Job Number ${env.BUILD_NUMBER}"
  echo "Jenkins Node Name ${env.NODE_NAME}"
  
  echo "Jenkins Home ${env.JENKINS_HOME}"
  echo "Jenkins URL ${env.JENKINS_URL}"
  echo "JOB Name ${env.JOB_NAME}"
  
  properties([
    buildDiscarder(logRotator(numToKeepStr: '3')),
    pipelineTriggers([
        pollSCM('* * * * *')
    ])
  ])
  
  def mavenHome=tool name: "maven 3.6.2", type: "maven"
    
  stage('CheckouttheCode') {
   git branch: 'master', credentialsId: '141a4bec-0ea2-4ae6-907e-1f053813fda9', url: 'https://github.com/jagadeswar219/maven-web-application.git'  
 }
  /*
   stage('Checkout'){
     checkout scm
  }
  */
 
 stage('Build')
 {
  sh  "${mavenHome}/bin/mvn clean package"
 }

 
 stage('Testing')
   {
    if(isUnix()){
     sh 'mvn test'
      }
      else{
       bat 'mvn test'   
      }
   }
 

 stage('SonarQubeReport')
 {
  sh  "${mavenHome}/bin/mvn sonar:sonar"
 }

  stage('UploadArtifactsIntoNexus')
 {
  sh  "${mavenHome}/bin/mvn deploy"
 }
 
 stage('DeplotoTomcat'){
     sh "cp $WORKSPACE/target/*.war /tmp/"
   echo "the user is ${env.BUILD_USER}"
     //sh "cp $WORKSPACE/target/*.war /opt/apache-tomcat-8.5.46/webapps/"
 }
 

/*stage('DeploytoTomcat'){

   sshagent(['9554f0b8-eda0-486d-9d23-ce7585c32f70']) 
   {
     sh "scp -o StrictHostKeyChecking=no target/maven-web-application.war ec2-user@13.235.70.188:/opt/apache-tomcat-9.0.22/webapps/maven-web-application.war"
   }
}*/
 stage('EmailNotification'){
    mail to: 'jagadeswar219@gmail.com',
         bcc: 'jagadeswar219@gmail.com', 
         cc: 'jagadeswar219@gmail.com', 
         from: 'jagadeswar219@gmail.com', 
         replyTo: 'jagadeswar219@gmail.com', 
         subject: 'Build Notification'
         body: 'Build Done, Please check the build log for more details..'
         
                  Regards,
                  jagadeswar reddy
                  
 }
 
 /*stage("SlackNotification"){
     slackSend baseUrl: 'https://devops-team-bangalore.slack.com/services/hooks/jenkins-ci/', channel: 'build-notification', message: 'Build done through', tokenCredentialId: '12797dc5-eb70-4f19-8e05-8c07bc58d79d'
 }*/
}
