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
            }
        }
        stage('Example') {
        if (env.BRANCH_NAME == 'master') {
            echo 'I only execute on the master branch'
        } else {
            echo 'I execute elsewhere'
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