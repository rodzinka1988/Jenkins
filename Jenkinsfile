pipeline {
    agent {
        docker { image 'node:latest' }
    }

    environment { 
            PROX ='elo'
        }
    
    stages {
        stage('Build install') {
            steps {
                 checkout([$class: 'GitSCM',
                    branches: [[name: '*/main']], 
                //     userRemoteConfigs: [[
                //     url: 'https://github.com/rodzinka1988/Jenkins.git',
                //     credentialsId: 'test'  // <-- Twój GitHub token w Jenkins
                // ]]
                sh 'ps -aux | grep java'
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