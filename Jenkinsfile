node{
    
    stage('Clone repo'){
       git credentialsId: 'GitRepo', url: 'https://github.com/amol97663/maven-web-app.git'
    }    
    
    stage('Maven Build'){     
       def mavenHome = tool name: "Maven-3.8.6", type: "maven"
       def mavenCMD = "${mavenHome}/bin/mvn"
       sh "${mavenCMD} clean package" 
        
    }

    stage('Code Review') {
       withSonarQubeEnv('Sonar-Server-8.9') {
        def mavenHome = tool name: "Maven-3.8.6", type: "maven"
        def mavenCMD = "${mavenHome}/bin/mvn"
        sh "${mavenCMD} sonar:sonar" 
           
    }    
       
    stage('Upload Build Artifact') {
        nexusArtifactUploader artifacts: [[artifactId: '01-maven-web-app', classifier: '', file: 'target/01-maven-web-app.war', type: 'war']], credentialsId: 'NexusCred', groupId: 'in.amolanarase', nexusUrl: '34.125.54.60:8081', nexusVersion: 'nexus3', protocol: 'http', repository: 'amol-snapshot-repository', version: '1.0-SNAPSHOT'
        
        
        }    
    }   
}



        
        
        
        
