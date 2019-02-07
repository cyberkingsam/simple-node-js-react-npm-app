def StagingPath = '/home/foodie/staging/'
def user
pipeline{
    agent any
    stages{
        stage('Input')
        {
            steps {
                script{
                     try{
                            timeout(time: 20, unit: 'SECONDS') {
                                env.RELEASE_SCOPE = input message: 'User input required', ok: 'Release!',
                                parameters: [choice(name: 'Deploy Options', choices: 'Php_deploy\nFast_deploy', description: 'How you want to deploy?')]
                            }
                        } catch(FlowInterruptedException)
                        {
                            user = FlowInterruptedException.getCauses()[0].getUser()
                            echo "${user}"
                        }
                }
            }

        }
        stage('Validating'){
            steps{
                script{
                    if ("${user}" == 'SYSTEM') {  // if it's system it's a timeout
                        echo "SYSTEM Timeout"
                    } 
                    else {  // if not and input is false it's the user
                        echo "Build aborted by: [${user}]"
                    }
                }
            }

        }
        
        stage('ZStagingDeploy'){
            steps{
                script{
                    if (env.RELEASE_SCOPE == 'Php_deploy') {
                        echo 'will do a php deploy and will take time'
                    }
                else {
                    echo 'will be faster'
                }
                }
                
            }
        }
    }
}