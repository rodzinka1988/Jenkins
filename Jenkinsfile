pipeline {
    agent any

    stages {
        stage('Build') {
            steps {
                sh 'ps -aux | grep java '
                environment { 
                    PROX='elo '
                }

                sh 'echo $PROX' > test.txt
            }

        
        }

    // post {
    //     always {
    //         archiveArtifacts artifacts: './test.txt', fingerprint: true
    //         junit './test.txt'
    //     }
    // }
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