# jenkinsfile for nexus repository uplaod

pipeline {   
    agent any
    tools {
        maven 'maven3'
    }
    stages{
        stage('git download'){   
            steps{
                git 'https://github.com/javahometech/simple-app.git'
            } 
        }
        stage('build'){
            steps{
            sh script: 'mvn clean package'
            }
        }
        stage('nexus uplaod'){          
            steps{
                script{
                    def mavenPom = readMavenPom file: 'pom.xml'  ##to dynamically change the version whenever their is a chnage in pom.xml version 
                    nexusArtifactUploader artifacts: [
                    [
                        artifactId: 'simple-app', 
                        classifier: '', 
                        file: "target/simple-app-${mavenPom.version}.war", 
                        type: 'war'
                        ]
                    ], 
                    credentialsId: 'Nexus3_cred', 
                    groupId: 'in.javahome', 
                    nexusUrl: '18.188.47.218:8081', 
                    nexusVersion: 'nexus3', 
                    protocol: 'http', 
                    repository: 'my-maven-nexus', 
                    version: "${mavenPom.version}"   #to dynamically change the version whenever their is a chnage in pom.xml version 
                    }
                }   
            }            
        }
   }

# references: to create this file
# 1. https://www.youtube.com/watch?v=p_Wo3aqUJto
# 2. https://www.youtube.com/watch?v=iegXZUGVkL8