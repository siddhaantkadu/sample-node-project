pipeline { 
    agent { 
        label 'JENKINS-AGENT-1' 
        }
    triggers { 
        pollSCM('* * * * *') 
        }

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
        stage('CleanUp Docker') { 
            steps { 
                sh '''
                 docker container rm -f $(docker container ls -qa)
                '''
            }
        }
        stage('Build Docker Image') { 
            steps { 
                sh '''
                    docker image build -t siddhaant/sample-node-project-${BUILD_NUMBER} .
                '''
            }
        }
        stage('Run Application') { 
            steps { 
                sh '''
                    docker container run -p 8443:3005 -d --name nodejs-${BUILD_NUMBER} siddhaant/sample-node-project-${BUILD_NUMBER} 
                '''
            }
        }
        stage('Validate Application') { 
            steps { 
                sh "docker container ls -a"
            }
        }
    }
}