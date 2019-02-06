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
        stage('production')
        {
            steps {
                echo 'working'
            }
        }

    }
}