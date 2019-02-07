def StagingPath = '/home/foodie/staging/'
pipeline{
    agent any
    stages{
        stage('Input')
        {
            steps {
                script{
                     try{
                            timeout(time: 20, unit: 'SECONDS') {
                                env.RELEASE_SCOPE = input message: 'User input required', ok: 'Deploy!',
                                parameters: [choice(name: 'Deploy Options', choices: 'Php_deploy\nFast_deploy', description: 'How you want to deploy?')]
                            }
                        } catch(FlowInterruptedException)
                        {
                             env.jenuser = FlowInterruptedException.getCauses()[0].getUser()
                            echo "${env.jenuser}"
                        }
                }
            }

        }
        stage('Validating'){
            steps{
                echo "${env.jenuser}"
                script{
                    if ("${env.jenuser}" == 'SYSTEM') {  // if it's system it's a timeout
                        echo "SYSTEM Timeout"
                    } 
                    else {  // if not and input is false it's the user
                        currentBuild.result = 'ABORTED'
                        error('Stopping early…')
                        echo "Build aborted by: [${env.jenuser}]"
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