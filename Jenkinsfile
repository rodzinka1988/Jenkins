pipeline {
    agent any

    environment { 
            PROX ='elo'
        }

    stages {
        stage('Build') {
            steps {
                sh 'ps -aux | grep java '
           
                sh "echo $PROX > test.txt"
            }

    
        }
        stage ('Test') {

            steps {
                copyArtifacts(projectName: 'rodzinka', filter:'test.txt', optional: true);
                sh ' cat test.txt'
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
        always {
            archiveArtifacts artifacts: 'test.txt', fingerprint: true, allowEmptyArchive: true
            // junit './test.txt'
        }

        success {
            echo "Pipeline succeeded"
        }
        failure {
            echo "Pipeline failed"
        }
    }


}