pipeline {
    agent any

    environment { 
            PROX ='elo'
        }

    stages {
        stage('Build install') {
            steps {
                sh 'ps -aux | grep java '
                sh "npm audit --audit-level=critical && echo $?"
                sh "echo $PROX > test.txt"
                stash name: 'my-artifact', includes: 'test.txt'
            }

    
        }
        stage ('Test') {

            steps {
                unstash 'my-artifact'
                sh ' cat test.txt && cat /etc/passwdvb '
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

    
    post {
        // always {
        //     archiveArtifacts artifacts: 'test.txt', fingerprint: true, allowEmptyArchive: true
        //     // junit './test.txt'
        // }

        success {
            echo "Pipeline succeeded"
        }
        failure {
            echo "Pipeline failed"
        }
    }


}