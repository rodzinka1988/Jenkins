pipeline {
    agent {
        docker { image 'node:24.11.1-alpine3.22' }
    }

    environment { 
            PROX ='elo'
        }
    
    stages {
        stage('Build install') {
            steps {

                sh 'ps -aux | grep java '
                sh 'dn install npm'
                sh "npm audit --audit-level=critical"
                sh "echo $PROX > test.txt"
                stash name: 'my-artifact', includes: 'test.txt'
            }

    
        }
        stage ('Test') {

            steps {
                unstash 'my-artifact'
                sh ' cat test.txt && cat /etc/passwd '
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