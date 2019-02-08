def StagingPath = '/home/foodie/staging/'
o2_menu_workers = ["process_pos_menu_update_requests_worker","process_dominos_menu_importer_queue","process_ccd_menu_importer_queue","process_mcd_menu_importer_queue","process_mast_kalandar_menu_importer","process_pizzahut_menu_importer","process_kfc_menu_importer","o2_copy_menu_worker"]
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
                    env.INTANCE_LABLE = "sng-${env.BRANCH_NAME}-stg"
                    echo "${env.INTANCE_LABLE}"
                    if ("${env.jenuser}" == 'SYSTEM') {  // if it's system it's a timeout
                        echo "SYSTEM Timeout"
                    } 
                    else if("${env.jenuser}" == 'null')
                    {
                        echo "user's input"
                    }
                    else {  
                        currentBuild.result = 'ABORTED'
                        error('Stopping early…')
                        echo "Build aborted by: [${env.jenuser}]"
                    }
                    //sh "echo stopped > state"
                    sh "aws  ec2 describe-instances --filter \"Name=tag:service,Values=staging-web\" \"Name=tag:Name,Values=${env.INTANCE_LABLE}\" --query \"Reservations[*].Instances[*].[State.Name]\" --region ap-southeast-1 --output text > state"
                    sh "aws  ec2 describe-instances --filter \"Name=tag:service,Values=staging-web\" \"Name=tag:Name,Values=${env.INTANCE_LABLE}\" --query \"Reservations[*].Instances[*].[InstanceId]\" --region ap-southeast-1 --output text > instanceid"
                    def output=readFile('state').trim()
                    def instanceid = readFile('instanceid').trim()
                    echo "${instanceid}"
                    echo "output=$output";
                    if("${output}"== 'stopped')
                    {   
                        sh "echo starting > res"
                        sh "aws ec2 start-instances --instance-ids ${instanceid}"
                        def time = 20
                        echo "Waiting ${time} seconds for deployment to complete prior starting smoke testing"
                        sleep time.toInteger()
                    }
                    else{
                        echo "already running"
                    }
                }
            }

        }
        stage('ZStagingDeploy'){
            steps{
                script{
                    o2_menu_workers.each { item ->
                            echo "Hello ${item}"
                        }
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