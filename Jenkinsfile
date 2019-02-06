pipeline{
    agent{
        docker{
            image 'node:6-alpine'
            args '-p 3000:3000'
        }
    }
    parameters {
        string(name: 'PERSON', defaultValue: 'Mr Jenkins', description: 'Who should I say hello to?')

        text(name: 'BIOGRAPHY', defaultValue: '', description: 'Enter some information about the person')

        booleanParam(name: 'TOGGLE', defaultValue: true, description: 'Toggle this value')

        choice(name: 'CHOICE', choices: ['One', 'Two', 'Three'], description: 'Pick something')

        password(name: 'PASSWORD', defaultValue: 'SECRET', description: 'Enter a password')

        file(name: "FILE", description: "Choose a file to upload")
    }
    stages{
         stage('Input') {
            steps {
                 echo "Hello ${params.PERSON}"

                echo "Biography: ${params.BIOGRAPHY}"

                echo "Toggle: ${params.TOGGLE}"

                echo "Choice: ${params.CHOICE}"

                echo "Password: ${params.PASSWORD}"
                script {
                    env.RELEASE_SCOPE = input message: 'User input required', ok: 'Release!',
                            parameters: [choice(name: 'Deploy Options', choices: 'Php_deploy\nFast_deploy', description: 'How you want to deploy?')]
                
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