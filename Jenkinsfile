pipeline{
    agent any
    stages{
        stage("Test"){
            agent{
                label "slave"
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