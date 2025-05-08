pipeline{
    agent any
    stages{
        stage("CheckOut"){
        agent{
                docker{
                   label "slave" 
                   image 'node:18-alpine' 
                   reuseNode true
                }
            }
            steps{
                checkout scmGit(branches: [[name: '*/main']], extensions: [], userRemoteConfigs: [[url: 'https://github.com/vdespa/learn-jenkins-app.git']])

            }
        }

        stage("npm test/Build"){
            agent{
                
                docker{
                   label "slave" 
                   image 'node:18-alpine' 
                }
            }

            steps{
                sh "npm install"
                sh "npm test"
                sh "npm run build"
            }
        }
    }
}