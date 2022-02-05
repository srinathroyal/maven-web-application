node{
 
 def mavenHome = tool name: "maven3.8.3"
 
 stage('checkoutcode')
 {
  git branch: 'development', credentialsId: '11443158-bcbc-4d83-bbec-997967b4cdfa', url: 'https://github.com/srinathroyal/maven-web-application.git'
 }
 
 stage('Build')
 {
  sh "${mavenHome}/bin/mvn clean package"
 }
 
 stage('Soreport')
 {
  sh "${mavenHome}/bin/mvn clean sonar:sonar"
 }
 
 stage('UploadArtifact')
 {
  sh "${mavenHome}/bin/mvn clean deploy"
 }
 
 stage('DeployToTomcat')
{
 sshagent(['630f34a9-3df8-4d2c-9987-2a1038ad7849']) {
  sh "scp -o StrictHostKeyChecking=no target/maven-web-application.war ec2-user@18.224.8.147:/opt/apache-tomcat-9.0.58/webapps"
}
}
    
}
