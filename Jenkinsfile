pipeline{
    agent{
        docker{
            image 'node:6-alpine'
            args '-p 3000:3000'
        }
    }
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
                        def user = err.getCauses()[0].getUser()

      if (user.toString == 'SYSTEM') {  // if it's system it's a timeout
        didTimeout = true
        echo "Build timed out at approval step"
      } else if (userInput == false) {  // if not and input is false it's the user
        echo "Build aborted by: [${user}]"
      }
                        
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

        if (env.NODE_NAME == 'master') {
            echo 'I only execute on the master branch'
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