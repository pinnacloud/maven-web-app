pipeline {
    agent any
    tools {
     maven 'Maven3.9.6'
    }


    stages {
        stage('Checkout Code') {
            steps {
                git branch: 'dev', credentialsId: 'af8322a3-29b9-4651-a517-6b898fc0af0f', url: 'https://github.com/pinnacloud/maven-web-app.git'
            }
        }
        stage('Build') {
            steps {
                sh "mvn clean package"
            }
        }
        
    }
}
