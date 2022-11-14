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
    }
}



        
        
        
        
