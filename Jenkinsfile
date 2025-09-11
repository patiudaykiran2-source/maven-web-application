node
{
    def MVH = tool name: "maven-3.9.11"
    stage('checkoutCode')
    {
        git credentialsId: 'fe7b2f3b-c823-47a2-9230-380127cd1a97', url: 'https://github.com/patiudaykiran2-source/maven-web-application.git'
    }
    stage('buildCode')
    {
        sh "${MVH}/bin/mvn package"
    }
    stage('sonarCheck')
    {
        sh "${MVH}/bin/mvn sonar:sonar"
    }
    stage('nexusRepo')
    {
        sh "${MVH}/bin/mvn deploy"
    }
    stage('DeployToTomcat')
    {
        deploy adapters: [tomcat9(alternativeDeploymentContext: '', credentialsId: 'tomcat', path: '', url: 'http://3.110.217.80:8080/')], contextPath: null, onFailure: false, war: '**/maven-web-application.war'
    }
}
