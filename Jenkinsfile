pipeline{
    agent{
        docker{
            image 'node:6-alpine'
            args '-p 3000:3000'
        }
    }
    stages{
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
                    def userInput
                    try {
                            userInput = input(
                            id: 'Proceed1', message: 'Was this successful?', parameters: [
                            [$class: 'BooleanParameterDefinition', defaultValue: true, description: '', name: 'Please confirm you agree with this']
                            ])
                        } catch(err) { // input false
                def user = err.getCauses()[0].getUser()
                userInput = false
                echo "Aborted by: [${user}]"
            }
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