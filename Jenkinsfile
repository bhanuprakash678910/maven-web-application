node
{
 def mavenHome = tool name: "maven3.6.3"
 stage('checkoutCode')
 {
   git branch: 'development', url: 'https://github.com/bhanuprakash678910/maven-web-application.git'
 } 
 stage('Build')
 {
  sh "${mavenHome}/bin/mvn clean package"
 }
 stage('ExecuteSonarQubeReport')
 {
  sh "${mavenHome}/bin/mvn sonar:sonar"
 }
  stage('UploadArtifactintoNexus')
 {
  sh "${mavenHome}/bin/mvn deploy"
 }
 stage('DeployAppIntoTomcat')
 {
  sshagent(['3ae47cba-8331-4a7c-ac99-fc66799c65a7'])
  {
   sh "scp -o StrictHostKeyChecking=no target/maven-web-application.war ec2-user@3.236.83.140:/opt/apache-tomcat-9.0.41/webapps/"
  }
 }
}
