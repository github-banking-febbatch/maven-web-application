node{
    
echo "The Job name is: ${env.JOB_NAME}"
echo "The build number is: ${env.BUILD_NUMBER}"
echo "The build id is: ${env.BUILD_ID}"
echo "The node name is: ${env.NODE_NAME}"
echo "The Job url is: ${env.JOB_URL}"

properties([buildDiscarder(logRotator(artifactDaysToKeepStr: '', artifactNumToKeepStr: '5', daysToKeepStr: '', numToKeepStr: '5')), [$class: 'JobLocalConfiguration', changeReasonComment: ''], pipelineTriggers([pollSCM('* * * * *')])])    

def mavenHome= tool name: 'maven3.8.8'

stage('CheckoutCode'){
git branch: 'development', credentialsId: '4e19960f-ea91-4a0f-b38e-8b35a607c29e', 
url: 'https://github.com/github-banking-febbatch/maven-web-application.git'
}
stage('Build'){
sh "${mavenHome}/bin/mvn clean package"
}
/*  
stage('ExecuteSonarQubeReport'){
sh "${mavenHome}/bin/mvn clean sonar:sonar"
}
stage('UploadArtifactsintoNexus'){
sh "${mavenHome}/bin/mvn clean deploy"
}
stage('DeployintoTomcat'){
sshagent(['7bedd85b-adda-4976-b56a-9588bd444996']) {
sh "scp -o StrictHostKeyChecking=no target/maven-web-application.war ec2-user@172.31.47.76:/opt/apache-tomcat-9.0.73/webapps"
}
}
*/
}
