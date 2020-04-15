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
                         '''
                       }   
                        }
                      }
                       stage('Deploy') 
                      {
                       steps 
                        {

                            sh '''
                            cd build
                            tar -xvf frontend-${BUILD_NUMBER}.tar
                            rm -rf frontend-${BUILD_NUMBER}.tar
                            ls -ltr
                            gsutil acl ch -u AllUsers:R gs://tanmay-kachariya
                            gsutil defacl set public-read gs://tanmay-kachariya
                            gsutil web set -m index.html -e index.html gs://tanmay-kachariya
                            gsutil cp -r * gs://tanmay-kachariya/
                            gsutil setmeta -h "content-type: image/svg+xml" gs://tanmay-kachariya/static/media/*.svg
                            '''
                         
                        }
                      }
                 }
              }
