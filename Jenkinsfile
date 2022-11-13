node{
    
    stage('Clone repo'){
        git credentialsId: 'bccf3250-d50c-45e5-ab27-3e76cf70d027', url: 'https://github.com/amol97663/maven-web-app.git'
    }
    
    stage('maven build'){
    def mavenHome = tool name: "Maven-3.8.6", type: "maven"
        def mavenCMD = "${mavenHome}/bin/mvn"
        sh "${mavenCMD} clean package"
    }
}
