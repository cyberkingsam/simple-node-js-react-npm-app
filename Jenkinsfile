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
                                parameters: [choice(name: 'Deploy Options', choices: 'Php_deploy\nFast_deploy\nmarinate_fast_deploy\nmarinate_php_deploy', description: 'How you want to deploy?')]
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
                                echo "Php_deploy"
                               //sh "cd ${StagingPath}${env.BRANCH_NAME}/Oven && ./Oven --no-color staging_php_deploy | tee -a ${StagingPath}${env.BRANCH_NAME}/hipchat.log"
                            }
                            else if(env.RELEASE_SCOPE == 'marinate_fast_deploy'){
                                echo "marinate fast deploy"
                               // sh "cd /home/foodie/staging/#{staging_name}/Oven && ./Oven --no-color no_pull_fast_deploy_with_marinate | tee -a /home/foodie/staging/#{staging_name}/hipchat.log"
                            }
                            else if(env.RELEASE_SCOPE == 'marinate_php_deploy'){
                                echo "marinate_php_deploy"
                                //sh "cd /home/foodie/staging/#{staging_name}/Oven && ./Oven --no-color staging_php_deploy_with_marinate | tee -a /home/foodie/staging/#{staging_name}/hipchat.log"
                            }
                            else {
                                echo "fast php deploy"
                                //sh "cd ${StagingPath}${env.BRANCH_NAME}/Oven && ./Oven --no-color no_pull_fast_deploy | tee -a ${StagingPath}${env.BRANCH_NAME}/hipchat.log"
                            }
                    }
                }  
            }
        }
    }
}