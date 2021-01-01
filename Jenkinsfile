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
        }

        stage('upload war to nexus repo') {
            steps {
                    script {
                        def mavenPom = readMavenPom file: 'pom.xml'
                         nexusArtifactUploader artifacts: [
                         [
                           artifactId: 'simple-app', 
                           classifier: '', 
                           file: "target/simple-app-${mavenPom.version}.war", 
                           type: 'war'
                            ]
                         ], 
                         credentialsId: 'nexus-creds',
                         groupId: 'in.javahome', 
                         nexusUrl: '172.31.14.81:8081', 
                         nexusVersion: 'nexus3', 
                         protocol: 'http', 
                         repository: 'simple-app', 
                         version: "${mavenPom.version}"
                    }
                 }
          }    
    }
}