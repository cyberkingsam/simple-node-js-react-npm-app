def StagingPath = '/home/foodie/staging/'
def user = 'i'
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
                            user1 = FlowInterruptedException.getCauses()[0].getUser()
                            echo "${user1}"
                        }
                }
            }

        }
        stage('Validating'){
            steps{
                echo "${user1}"
                script{
                    if ("${user1}" == 'SYSTEM') {  // if it's system it's a timeout
                        echo "SYSTEM Timeout"
                    } 
                    else {  // if not and input is false it's the user
                        echo "Build aborted by: [${user1}]"
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
    post {
        always {
            sh "curl \'https://oapi.dingtalk.com/robot/send?access_token=e30bce18c67b9fa0a663a9925afa3e490c16e5aaee068a69b0d14b1ffe0ee98a\' -H \'Content-Type:application/json\' -d \'{\"msgtype\": \"text\", \"text\": {\"content\": \"${StagingPath}aa102\"}}\'"
        }
        failure {
            sh "curl \'https://oapi.dingtalk.com/robot/send?access_token=e30bce18c67b9fa0a663a9925afa3e490c16e5aaee068a69b0d14b1ffe0ee98a\' -H \'Content-Type:application/json\' -d \'{\"msgtype\": \"text\", \"text\": {\"content\": \"Build Fail\"}}\'"
        }
        success{
             sh "curl \'https://oapi.dingtalk.com/robot/send?access_token=e30bce18c67b9fa0a663a9925afa3e490c16e5aaee068a69b0d14b1ffe0ee98a\' -H \'Content-Type:application/json\' -d \'{\"msgtype\": \"text\", \"text\": {\"content\": \"Build Success\"}}\'"
        }
    }
}