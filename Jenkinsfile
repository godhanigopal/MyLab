pipeline{
    //Directives
    agent any
    tools {
        maven 'maven'
    }
    environment{
        ArtifactId = readMavenPom().getArtifactId()
        Version = readMavenPom().getVersion()
        Name = readMavenPom().getName()
        GroupID = readMavenPom().getGroupId()
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
                script{
                    def NexusRepo = Version.endsWith("SNAPSHOT") ? "GopalDevOpsLab-SNAPSHOT" : "GopalDevOpsLab-Release"
                
                nexusArtifactUploader artifacts: [[
                    artifactId: "${ArtifactId}", 
                    classifier: '', 
                    file: "target/${ArtifactId}-${Version}.war", 
                    type: 'war']], 
                    credentialsId: '637f999a-549f-435d-8d76-4ac6ce5334d3', 
                    groupId: "${GroupID}", 
                    nexusUrl: '172.20.10.113:8081', 
                    nexusVersion: 'nexus3', 
                    protocol: 'http', 
                    repository: "${NexusRepo}", 
                    version: "${Version}"
            }
        }
        }
        // Stage 4: Print some information
        stage ('Print Enviroment Variable'){
            steps {
                echo "ArtifactID is '${ArtifactId}'"
                echo "Version is '${Version}'"
                echo "GroupID is '${GroupID}'"
                echo "Name is '${Name}'"
            }
        }

        // Stage 5: Deploying
        stage('Deploy'){
            steps {
                echo "deploying......"
            }
        }
    
        // // Stage3 : Publish the source code to Sonarqube
        // stage ('Sonarqube Analysis'){
        //     steps {
        //         echo "deploying......"
        //         // echo ' Source code published to Sonarqube for SCA......'
        //         // withSonarQubeEnv('sonarqube'){ // You can override the credential to be used
        //         //      sh 'mvn sonar:sonar'
        //         //}

        //     }
        // }
        
    }

}