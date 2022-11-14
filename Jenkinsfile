node{
    
    stage('Clone repo'){
        git credentialsId: 'bccf3250-d50c-45e5-ab27-3e76cf70d027', url: 'https://github.com/amol97663/maven-web-app.git'
    }
    
    stage('maven build'){
        def mavenHome = tool name: "Maven-3.8.6", type: "maven"
        def mavenCMD = "${mavenHome}/bin/mvn"
        sh "${mavenCMD} clean package"
    }
    
    stage('Code Review') {
    withSonarQubeEnv('sonarserver') {
        def mavenHome = tool name: "Maven-3.8.6", type: "maven"
        def mavenCMD = "${mavenHome}/bin/mvn"
        sh "${mavenCMD} sonar:sonar"
        }
        
    stage('Upload Build Artifact') {
        nexusArtifactUploader artifacts: [[artifactId: '01-maven-web-app', classifier: '', file: 'target/01-maven-web-app.war', type: 'war']], credentialsId: 'Nexus cred', groupId: 'in.amolanarase', nexusUrl: '34.125.54.60:8081', nexusVersion: 'nexus3', protocol: 'http', repository: 'amolanarase-snapshot-repository', version: '1.0-SNAPSHOT'
        }
        
        stage('deploy') {
       // sshagent(['tomcat-server-agent']) {
   // sh 'scp -o StrictHostKeyChecking=no target/01-maven-web-app.war tomcat-server@34.125.145.213:/opt/tomcat/webapps'
            deploy adapters: [tomcat9(credentialsId: 'Tomcat', path: '', url: 'http://34.125.206.136/')], contextPath: 'target/', onFailure: false, war: '"**/*.war"'
        }
       
        }
    }
    }
        
        
        
        
