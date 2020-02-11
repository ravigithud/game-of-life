pipeline 
{
agent any
tools
{
maven "Maven"
}
stages {
stage('Gitcheckout')
{
steps{
git credentialsId: 'github', url: 'https://github.com/ravigithud/game-of-life.git'
}
}
stage('Maven conf')
{
steps {
sh label: '', script: 'mvn install'
}
}
stage ('Nexus storage')
{
steps {
nexusPublisher nexusInstanceId: '9000', nexusRepositoryId: 'releases', packages: [[$class: 'MavenPackage', mavenAssetList: [[classifier: '', extension: '', filePath: '/var/lib/jenkins/workspace/Complete Pipeline Project/gameoflife-web/target/gameoflife.war']], mavenCoordinate: [artifactId: 'game-of-life', groupId: 'ADP', packaging: 'war', version: '$BUILD_ID']]]
}
}
stage ('TomcatServer')
{
steps {
deploy adapters: [tomcat8(credentialsId: '123', path: '', url: 'http://13.232.122.56:8080/')], contextPath: null, war: '**/*.war'
    }
  }
 }
}


