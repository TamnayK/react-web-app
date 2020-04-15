 pipeline 
               {
                   agent any    
                   tools
                   {
                       
                       nodejs  'node'

                   }
                   stages 
                    {
                      stage('Build') 
                      {
                       steps 
                        {
                          script
                          {   
                           cleanWs()
                           checkout changelog: false, poll: false, scm: [$class: 'GitSCM', branches: [[name: '${Repo_branch}']], doGenerateSubmoduleConfigurations: false, extensions: [], submoduleCfg: [], userRemoteConfigs: [[credentialsId: 'github_credential', url: 'https://github.com/vmgponly/react-web-app.git']]]
                         
                         sh '''
                         node --version
                         npm --version
                         
                         npm install
                         npm run build
                         ls -ltr
                         cd build/
                         tar -cvf frontend-${BUILD_NUMBER}.tar *
                         cp frontend-${BUILD_NUMBER}.tar ${WORKSPACE}/
                         ls -ltr
                         '''
                       }   
                        }
                      }
                       stage('Deploy') 
                      {
                       steps 
                        {

                            sh '''
                           rm -rf deploy
                           mkdir deploy
                           cp -r tar frontend-${BUILD_NUMBER}.tar deploy/
                           cd deploy
                           tar -xvf frontend-${BUILD_NUMBER}.tar                            
                            ls -ltr                            
                            '''
                         
                        }
                      }
                 }
              }
