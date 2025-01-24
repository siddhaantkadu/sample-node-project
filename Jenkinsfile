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
        stage('CleanUp Docker') { 
            steps { 
                sh '''
                    docker container rm -f $(docker ps -aq) 
                    docker image rm -f $(docker images -aq)
                    docker rmi -f $(docker images -aq)
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