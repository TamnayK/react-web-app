pipeline
{
agent any
  
  tools
    {
    nodejs 'node'
      
    }
  stages
  {
  stage('Build')
    {
     steps
      {
      script
        {
        checkout changelog: false, poll: false, scm: [$class: 'GitSCM', branches: [[name: '*/master']], doGenerateSubmoduleConfigurations: false, extensions: [], submoduleCfg: [], userRemoteConfigs: [[credentialsId: 'github_credentials', url: 'https://github.com/TamnayK/react-web-app.git']]]
        
        }
        
      }
    }
  
  }
  
  
  
}
