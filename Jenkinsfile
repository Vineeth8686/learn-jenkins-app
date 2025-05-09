pipeline{
    agent none
    stages{
        stage("Echo"){
          agent {
                docker {
                    label 'slave'
                    image 'node:18-alpine'
                }
           }  

            steps{
                echo "This is from Echo Stage"
            }
        }

        stage("Test"){
           agent {
                docker {
                    label 'slave'
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

        stage("E2E"){
            agent{
                docker{
                    label "slave"
                    image 'mcr.microsoft.com/playwright:v1.39.0-jammy'
                    
                }
            }
            steps{
                sh '''
                    npm install serve
                    node_modules/.bin/serve -s build &
                    sleep 10
                    npx playwright test
                '''
            }
        }
    }
    post{
        agent {
                docker {
                    label 'slave'
                    image 'node:18-alpine'
                }
           }
        always{
            junit 'jest-results/junit.xml'
        }
    }
}