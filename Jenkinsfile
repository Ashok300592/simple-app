pipeline {
    agent any
    tools {
  maven 'maven'
    }
    stages {
        stage('build') {
            steps {
                sh 'mvn clean package'
            }

        stage('upload war to nexus repo') {
            steps {
                nexusArtifactUploader artifacts: [
                    [
                        artifactId: 'simple-app', 
                        classifier: '', 
                        file: 'target/simple-app-1.0.0.war', 
                        type: 'war'
                        ]
                    ], 
                     credentialsId: 'nexus-creds',
                     groupId: 'in.javahome', 
                     nexusUrl: '172.31.14.81:8081', 
                     nexusVersion: 'nexus3', 
                     protocol: 'http', 
                     repository: 'http://35.154.196.171:8081/repository/simple-app/', 
                     version: '1.0.0'
                 }
          }    
        }
    }
}