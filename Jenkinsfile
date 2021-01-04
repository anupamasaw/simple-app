pipeline {
    agent any
    tools {
        maven 'maven3'
    }
    options {
        buildDiscarder logRotator(daysToKeepStr: '5', numToKeepStr: '7')
    }
    stages{
        stage('Build'){
            steps{
                 sh script: 'mvn clean package'
                 archiveArtifacts artifacts: 'target/*.war', onlyIfSuccessful: true
            }
        }
        stage('Upload War To Nexus'){
            steps{ 
                  nexusArtifactUploader artifacts: [
                      [
                          artifactId: 'simple-app', 
                          classifier: '', 
                          file: 'target/simple-app-1.0.0.war', 
                          type: 'war'
                      ]
                  ],
                  credentialsId: 'nexus3', 
                  groupId: 'in.javahome',
                  nexusUrl: '172.31.43.43:8081', 
                  nexusVersion: 'nexus3',
                  protocol: 'http', 
                  repository: 'http://3.18.112.41:8081/repository/simpleapp-release/', 
                  version: '1.0.0'
                    }
            }
        }
    }
}
