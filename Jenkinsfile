pipeline { 
    agent { label 'JENKINS-AGENT-1' }

    stages { 
        stage('SCM Checkout') { 
            steps { 
                git url: 'https://github.com/siddhaantkadu/sample-node-project.git', 
                    branch: 'master'
            }
        }
        stage('NPM Install') { 
            steps { 
                sh '''
                npm install 
                '''
            }
        }
        stage('Start NodeJS Application') { 
            steps { 
                    sh 'npm start'
            }
        }
    }
}