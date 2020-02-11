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
  }
 }

