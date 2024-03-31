node {
    echo "The Jobname is : ${JOB_NAME}"
    echo "The Buildno is : ${BUILD_NUMBER}"
    echo "The node name is : ${NODE_NAME}"
    echo "The Jenkins Home Directory is : ${JENKINS_HOME}"
    properties([buildDiscarder(logRotator(artifactDaysToKeepStr: '', artifactNumToKeepStr: '5', daysToKeepStr: '', numToKeepStr: '5')), [$class: 'JobLocalConfiguration', changeReasonComment: ''], pipelineTriggers([pollSCM('* * * * *')])])
    
    
    def mavenHome = tool name: 'Maven3.9.6'
stage('checkout code'){
git branch: 'dev', credentialsId: 'af8322a3-29b9-4651-a517-6b898fc0af0f', url: 'https://github.com/pinnacloud/maven-web-app.git'
}
stage('Build'){
 sh "${mavenHome}/bin/mvn clean package"
}
stage('execute sonarqube report'){
 sh "${mavenHome}/bin/mvn clean sonar:sonar"
}
stage('upload artifact to nexus'){
 sh "${mavenHome}/bin/mvn clean deploy"
}
stage('Deploy to Tomcat'){
 sshagent(['50480fd8-6d8b-44a2-965a-2307ad98d4b3']) {
 sh "scp -o StrictHostKeyChecking=no target/maven-web-application.war ec2-user@172.31.8.77:/opt/apache-tomcat-9.0.86/webapps/"
}
}
}
