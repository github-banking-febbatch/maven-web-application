node{
properties([buildDiscarder(logRotator(artifactDaysToKeepStr: '', artifactNumToKeepStr: '5', daysToKeepStr: '', numToKeepStr: '5')), [$class: 'JobLocalConfiguration', changeReasonComment: ''], pipelineTriggers([pollSCM('* * * * *')])])    
def mavenHome = tool name: 'maven3.8.8'    
stage('CheckoutCode'){
git branch: 'development', credentialsId: '51f8ab28-26bd-43d6-ae6b-c023c50ab9f5', url: 'https://github.com/github-banking-febbatch/maven-web-application.git'
}
stage('Build'){
sh "${mavenHome}/bin/mvn clean package"
}
stage('ExecuteSonarQubeReport'){
sh "${mavenHome}/bin/mvn sonar:sonar"
}
stage('UploadArtifactsintoNexus'){
sh "${mavenHome}/bin/mvn deploy"
}
stage('DeployAppintoTomcat'){
sshagent(['2250d1b3-4692-4c1f-9e5a-93cd277b0e7d']) {
sh "scp -o StrictHostKeyChecking=no target/maven-web-application.war ec2-user@172.31.41.109:/opt/apache-tomcat-9.0.83/webapps/"
}
}
}
