pipeline {

    agent any

    stages {

        stage("Git Checkout"){
            steps {
                git branch: 'main', url: 'https://github.com/rahulgusain2511/java-app.git'
            }
        }

        stage("Unit Testing"){
            steps {
                sh 'mvn test'
            }
        }

        stage("Integration Testing"){
            steps {
                sh 'mvn verify -DskipUnitTests'
            }
        }

        stage("Build"){
            steps {
                sh 'mvn clean install'
            }
        }
/*
        stage("Static Code Analysis"){
            steps {
                script {
                    withSonarQubeEnv(credentialsId: 'sonarqube1') {
                        sh 'mvn clean package sonar:sonar'
                    }
                }
            }
        }

        stage("Quality Gate Analysis"){
            steps {
                script {
                   waitForQualityGate abortPipeline: false, credentialsId: 'sonarqube' 
                }
            }
        }*/

        stage("Upload Artifacts to Nexus"){
            steps {
                script {
                   nexusArtifactUploader artifacts:
                    [[
                    artifactId: 'springboot',
                    classifier: '',
                    file: 'target/UPES.jar',
                    type: 'jar'
                    ]], 
                    credentialsId: 'nexusid', 
                    groupId: 'com.example', 
                    nexusUrl: '13.50.14.153:8081', 
                    nexusVersion: 'nexus2', 
                    protocol: 'http', 
                    repository: 'java-release', 
                    version: '1.0.0'
                }
            }
        }
    }
}
