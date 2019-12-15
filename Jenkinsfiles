node 
{
    def mavenHome = tool name: "maven.3.6.2"
    stage("Git")
    {
        git branch: 'development', credentialsId: '38f36948-2585-47a1-a63e-a638a92d85a1', url: 'https://github.com/SrujanReddyMR/maven-web-application.git'
    }
    stage("Maven")
    {
        sh "${mavenHome}/bin/mvn package"
    }
    stage("Sonar")
    {
        sh "${mavenHome}/bin/mvn sonar:sonar"
    }
    stage("Nexus")
    {
        sh "${mavenHome}/bin/mvn deploy"
    }
    stage("Tomcat")
    {
        sshagent(['9aa04958-fe0d-4ba1-92a0-6ca7376e2475'])
        {
            sh "scp -o StrictHostKeyChecking=no target/maven-web-application.war ec2-user@13.232.79.216:/opt/apache-tomcat-9.0.29/webapps/"
    
        }
    }
    
}
