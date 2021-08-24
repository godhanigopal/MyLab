pipeline{
    //Directives
    agent any
    tools {
        maven 'maven'
    }

    stages {
        // Specify various stage with in stages

        // stage 1. Build
        stage ('Build'){
            steps {
                sh 'mvn clean install package'
            }
        }

        // Stage2 : Testing
        stage ('Test'){
            steps {
                echo ' testing......'

            }
        }

        // Stage 3 : Publish the artifacts to Nexus Server
        stage('Publish artifacts to Nexus'){
            steps{
                nexusArtifactUploader artifacts: [[artifactId: 'GopalDevOpsLab', classifier: '', file: 'target/GopalDevOpsLab-0.0.5.war', type: 'war']], credentialsId: '637f999a-549f-435d-8d76-4ac6ce5334d3', groupId: 'com.gopaldevopslab', nexusUrl: '172.20.10.113:8081', nexusVersion: 'nexus3', protocol: 'http', repository: 'GopalDevOpsLav-SNAPSHOT', version: '0.0.5'
            }
        }

        // Stage3 : Publish the source code to Sonarqube
        stage ('Sonarqube Analysis'){
            steps {
                echo "deploying......"
                // echo ' Source code published to Sonarqube for SCA......'
                // withSonarQubeEnv('sonarqube'){ // You can override the credential to be used
                //      sh 'mvn sonar:sonar'
                //}

            }
        }

        
        
    }

}