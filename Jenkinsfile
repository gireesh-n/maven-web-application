node{
    def mavenHome = tool name:"maven3.8.2"
    stage('CheckOutCode'){
     git branch: 'development', credentialsId: '5191a68d-9a29-4e1e-8648-10eb8cbeec92', url: 'https://github.com/gireesh-n/maven-web-application.git'   
    }
    stage('Bulid'){
        sh "${mavenHome}/bin/mvn clean package"
    }
    stage('ExecuteSonarQubeReport'){
        sh "${mavenHome}/bin/mvn clean sonar:sonar"
    }
    stage('UploadArtificateIntoNexusRepo'){
        sh "${mavenHome}/bin/mvn clean deploy"
    }
    stage('DeployTheApplicationIntoTomcat'){
        sshagent(['fc89b601-4b53-4795-8869-6980818086d5']) {
    sh "scp -o strictHostkeychecking=no target/maven-web-application.war ec2-user@13.233.216.48:/opt/apache-tomcat-9.0.53/webapps"
}
    }
    stage('SendEmailNotification'){
       mail bcc: 'gowdgirish7@gmail.com', body: '''Build over!!

Regards,
Gireesh
8328096158''', cc: 'gowdgirish7@gmail.com', from: '', replyTo: '', subject: 'Build over!!', to: 'gowdgirish7@gmail.com'
    }
    
}    
    

