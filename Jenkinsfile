node{
    
    stage('Maven Build'){
        def mavenHome = tool name: "Maven-3.9.2", type: "maven"
        def mavenCMD = "${mavenHome}/bin/mvn"
        sh "${mavenCMD} clean package"
    }
        
    stage('Upload Build Artifact'){
        nexusArtifactUploader artifacts: [[artifactId: '01-maven-web-app', classifier: '', file: 'target/01-maven-web-app.war', type: 'war']], credentialsId: 'Nexus-Credentials', groupId: 'in.version', nexusUrl: 'nexus.ciurea.online', nexusVersion: 'nexus3', protocol: 'https', repository: 'maven-snapshot-repo', version: '1.0-SNAPSHOT'
    }
    
    
    
    
    
    
    stage('Deploy'){
        sshagent(['Tomcat-Agent']) {
            sh 'scp -o StrictHostKeyChecking=no target/01-maven-web-app.war ubuntu@44.201.243.208:/opt/tomcat/apache-tomcat-9.0.75/webapps'
        }
    }  

}
