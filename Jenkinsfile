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
      
//stage('sonarqube') {
  //environment 
  //{
   //def scannerHome = tool 'sonarqube'
    //}
   //steps {
     //   withSonarQubeEnv('sonarqube') {
       //sh "${scannerHome}/bin/sonar-scanner"
//}
  //  timeout(time: 10, unit: 'MINUTES') {
    // waitForQualityGate abortPipeline: true
     //}
	//  }
      //}
	
	stage ('Nexus storage')
	{
		steps {
nexusPublisher nexusInstanceId: '9000', nexusRepositoryId: 'releases', packages: [[$class: 'MavenPackage', mavenAssetList: [[classifier: '', extension: '', filePath: '/var/lib/jenkins/workspace/COP/gameoflife-web/target/gameoflife.war']], mavenCoordinate: [artifactId: 'game', groupId: 'oracle', packaging: 'war', version: '$BUILD_ID']]]
}
}
stage ('Deploy war')
{
steps {
sh label: '', script: 'ansible-playbook deploy.yml'
    }
  }
 }
}
