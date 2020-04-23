
node
{
  properties([[$class: 'JiraProjectProperty'], buildDiscarder(logRotator(artifactDaysToKeepStr: '', artifactNumToKeepStr: '5', daysToKeepStr: '', numToKeepStr: '5')), pipelineTriggers([cron('* * * * *')])])
    
     def mavenHome= tool name:"maven3.6.2"
     stage("checkoutttt ")
     {
         git credentialsId: '068b4029-0f9e-4623-a5e9-7bb6a06554a8', url: 'https://github.com/gprasanth1994/maven-web-application.git'
     }
     stage("build")
     {
         sh "${mavenHome}/bin/mvn clean package "
     }
      stage("sonarQube report")
     {
         sh "${mavenHome}/bin/mvn sonar:sonar "
     }
     /*
       stage("backup in nexus")
     {
         sh "${mavenHome}/bin/mvn deploy"
     }
     */
     stage("deploy into tomcat")
      {
          sshagent(['5bf0efda-d3a3-4cfb-989d-b9b5fa804efb']) 
          {
              sh "scp -o StrictHostKeyChecking=no target/maven-web-application.war ec2-user@13.232.54.34:/opt/apache-tomcat-9.0.34/webapps"
   
          }
      }
    
   
}
/*
node
{

  def mavenHome=tool name: "maven3.6.3"
  
 stage('Checkout')
 {
 	git branch: 'development', credentialsId: 'bed5a851-d84d-412e-87e7-bf9ce23c0e0e', url: 'https://github.com/MithunTechnologiesDevOps/maven-web-application.git'
 
 }
 /*
 stage('Build')
 {
 sh  "${mavenHome}/bin/mvn clean package"
 }
 
 stage('ExecuteSoanrQubeReport')
 {
 sh  "${mavenHome}/bin/mvn sonar:sonar"
 }
 
 stage('UploadArtifactintoNexus')
 {
 sh  "${mavenHome}/bin/mvn deploy"
 }
 
 stage('DeployAppintoTomcat')
 {
 sshagent(['cd93d61f-2d0f-4c60-8b33-34cf4fa888b0']) {
  sh "scp -o StrictHostKeyChecking=no target/maven-web-application.war ec2-user@13.235.132.183:/opt/apache-tomcat-9.0.29/webapps/"
 }
 }
*/
 stage('SendEmailNotification')
 {
 emailext body: '''Build is over..

 Regards,
 Mithun Technologies,
 9980923226.''', subject: 'Build is over', to: 'devopstrainingblr@gmail.com'
 }
}
*/
