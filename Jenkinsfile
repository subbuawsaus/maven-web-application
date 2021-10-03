node
{
    def mavenHome = tool name: "maven3.8.2"
    stage("checkout")
    {
        git branch: 'development', credentialsId: '39b49ba0-2a02-4e44-ad29-a73db259642f', url: 'https://github.com/subbuawsaus/maven-web-application.git'
    }
    stage('Build')
    {
        if(isUnix()){
            
       sh "$mavenHome/bin/mvn clean package"
        }
        else{
            bat "mvn clean package"
        }
            
    }
    stage("Deploy to Tomcat"){
        if(isUnix()){
        sshagent(['f2e9d870-df0c-4c2c-a051-98f217a46a30']) {
            sh "scp -o StrictHostKeyChecking=no target/maven-web-application.war ec2-user@3.17.186.35:/u01/app/Tomcat/apache-tomcat-9.0.53/webapps"
             }
        }
        else {
            bat 'cp target\\maven-web-application.war "C:\\Subbu\\Study\\Mith\\DevOPS\\Tomcat\\apache-tomcat-9.0.53\\webapps"'
        }
    }/*
    stage('Send Email'){
        emailext body: '''Build Over buddy and Success

regards
Subbu''', recipientProviders: [buildUser()], subject: 'Build Over', to: 'smptnpsc@gmail.com'
    }
    */
}
