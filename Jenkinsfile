pipeline{
    agent any
    stages{
        stage("Test"){
           agent {
                docker {
                    label "slave"
                    image 'node:18-alpine'
        }
           }

            steps {
                sh '''
                    ls -la
                    node --version 
                    npm --version
                    npm ci
                    npm run build
                    ls -la
                  '''
            }

        
    
        }
    }
}