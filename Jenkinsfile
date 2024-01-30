node {
    //def mavenHome=tool name: 'maven 3.9.6'
    def mavenHome=tool name: 'maven 3.9.6'
    stage ('checkout') {
        git branch: 'development', credentialsId: 'f7c27ddf-6e94-4437-918a-29dc7389c511', url: 'https://github.com/ibmprivate-limited/maven-web-application.git'
        }// checkout closing
        stage ('build') {
            sh "${mavenHome}/bin/mvn clean package"
        }//build closing
    
stage ('sonarqube testing')
    {
    sh "${mavenHome}/bin/mvn sonar:sonar"
    } //test closing
stage ('nexus arifact')
      {
    sh "${mavenHome}/bin/mvn deploy"
      } //nexus closing
      stage ('deploy')
      {
          sshagent(['8f6b41e3-1e48-4bc4-a618-b43cdd9678ea'])
          {
    // some block
    sh "scp -o StrictHostKeyChecking=no target/maven-web-application.war ec2-user@172.31.13.143:/opt/apache-tomcat-9.0.85/webapps/"
}
      }
}
