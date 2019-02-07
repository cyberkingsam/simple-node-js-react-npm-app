def path = '/home/foodie/staging/'

pipeline{
    agent any
    stages{
         stage('Input') {
            steps {
                script {
                    try{
                        timeout(time: 20, unit: 'SECONDS') {
                        env.RELEASE_SCOPE = input message: 'User input required', ok: 'Release!',
                            parameters: [choice(name: 'Deploy Options', choices: 'Php_deploy\nFast_deploy', description: 'How you want to deploy?')]
                    }
                    } catch(FlowInterruptedException)
                    {
                        def user = FlowInterruptedException.getCauses()[0].getUser()
                        echo "${user}"

    //   if (user.toString == 'SYSTEM') {  // if it's system it's a timeout
    //     didTimeout = true
    //     echo "Build timed out at approval step"
    //   } else if (userInput == false) {  // if not and input is false it's the user
    //     echo "Build aborted by: [${user}]"
    //   }
                        
                    } 
                echo "${env.RELEASE_SCOPE}"
                if (env.RELEASE_SCOPE == 'Php_deploy') {
                    echo 'will do a php deploy and will take time'
                }
                else {
                    echo 'will be faster'
                }
                }
            }
         }
        //  stage('If Proceed is clicked') {
        //     steps {
        //         print('hello')
        //     }
        // }
        stage('Build'){
            steps {
                echo 'checking'
            }
        }
        stage('Deploy')
        {
            steps {
                echo 'sameer saxena'
                sh 'printenv'
                sh 'echo $GIT_COMMIT >> test.log'
                script{
            stage('Example') {

        if (env.BRANCH_NAME == 'aa101') {
            echo "${path}"
            sh "cd ${path}aa101/ && echo test >> test.log"
            sh "curl 'https://oapi.dingtalk.com/robot/send?access_token=e30bce18c67b9fa0a663a9925afa3e490c16e5aaee068a69b0d14b1ffe0ee98a' -H 'Content-Type:application/json' -d '{"msgtype": "text", "text": {"content": "${path}aa101"}}' "
        } else {
            echo 'I execute elsewhere'
        }

        if (env.BRANCH_NAME == 'aa102') {
            echo "${path}"
            sh "cd ${path}aa102/ && echo test >> test.log"
            sh "curl 'https://oapi.dingtalk.com/robot/send?access_token=e30bce18c67b9fa0a663a9925afa3e490c16e5aaee068a69b0d14b1ffe0ee98a' -H 'Content-Type:application/json' -d '{"msgtype": "text", "text": {"content": "${path}aa102"}}' "
        } else {
            echo 'I execute elsewhere'
        }

        if (env.BRANCH_NAME == 'master') {
            echo "master branch do nothing"
        } else {
            echo 'I execute elsewhere'
        }
        }
        
    }
            }
        }
        stage('production')
        {
            steps {
                echo 'working'
            }
        }

    }
}