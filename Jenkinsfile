pipeline {
    agent any

    stages {
        stage('Build') {
            steps {
                sh 'ps -aux | grep java '
                environment { 
                    PROX= 'elo '
                }

                sh 'echo $PROX'
            }
        }
        // stage('Test') {
        //     steps {
        //         echo 'Testing..'
        //     }
        // }
        // stage('Deploy') {
        //     steps {
        //         echo 'Deploying....'
        //     }
        // }
    }
}