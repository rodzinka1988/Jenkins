pipeline {
    agent any

    environment { 
            PROX ='elo'
        }
    
    stages {
        stage('Checkout') {
            steps {
                checkout scmGit(
                    branches: [[name: '*/main']],
                    userRemoteConfigs: [[
                        url: 'https://github.com/rodzinka1988/Jenkins.git',
                        credentialsId: 'tw'
                    ]]
                )
            }
        }
               stage('Create package.json') {
            steps {
                sh '''
                    cat > package.json << 'EOF'
{
  "name": "rodzinka2",
  "version": "1.0.0",
  "description": "",
  "main": "index.js",
  "scripts": {
    "start": "node index.js",
    "test": "echo \\"Error: no test specified\\" && exit 1"
  },
  "keywords": [],
  "author": "",
  "license": "ISC",
  "dependencies": {}
}
EOF
                '''
            stash name: 'my-package', includes: 'package.json'


            }
        }
        stage('Build install') {
              agent {
                docker { image 'node:latest' }
            }
            
            steps {
                //  checkout([$class: 'GitSCM',
                //     branches: [[name: '*/main']], 
                // //     userRemoteConfigs: [[
                // //     url: 'https://github.com/rodzinka1988/Jenkins.git',
                // //     credentialsId: 'test'  // <-- Twój GitHub token w Jenkins
                // // ]]
                script {
                    def fristNames = "Paweł"  
                    echo fristNames   
                }
                unstash 'my-package'
                sh "ls -l"
                sh "npm install"
                sh "npm audit --audit-level=critical"
                sh "echo $PROX > test.txt"

                copyArtifacts(
                    projectName: 'Create package.json',  // Nazwa poprzedniego joba
                    filter: 'package.json',      // Które pliki skopiować
                    target: './package.json',      // Gdzie skopiować
                    selector: lastSuccessful() // Ostatni udany build
                )
               
            }

    
        }
        stage ('Test') {

            steps {
              
                sh 'echo Zrobione'
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