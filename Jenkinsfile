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
                    else {  
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
                    if (env.BRANCH_NAME == 'master') {
                        echo "do nothing"
                    }
                    else{
                            if (env.RELEASE_SCOPE == 'Php_deploy') {
                               sh "cd ${StagingPath}${env.BRANCH_NAME}/Oven && ./Oven --no-color staging_php_deploy | tee -a ${StagingPath}${env.BRANCH_NAME}/hipchat.log"
                            }
                        else {
                                sh "cd ${StagingPath}${env.BRANCH_NAME}/Oven && ./Oven --no-color no_pull_fast_deploy | tee -a ${StagingPath}${env.BRANCH_NAME}/hipchat.log"
                            }
                    }
                }  
            }
        }
    }
}