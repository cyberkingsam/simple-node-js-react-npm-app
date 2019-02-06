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
                echo ${env.BRANCH_NAME}
                echo '$GIT_BRANCH'
                echo '$GIT_URL'
            }
        }
        stage('production')
        {
            steps {
                echo 'Production'
            }
        }

    }
}