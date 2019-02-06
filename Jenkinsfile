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
                    env.RELEASE_SCOPE = input message: 'User input required', ok: 'Release!',
                            parameters: [choice(name: 'RELEASE_SCOPE', choices: 'patch\nminor\nmajor', description: 'What is the release scope?')]
                }
                echo "${env.RELEASE_SCOPE}"
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