pipeline {
    agent none

    stages {
    
        stage('Build') {
            agent {
                docker {
                    image 'node:18-alpine'
                    reuseNode true
                    label 'agent'
                }
            }
            steps {
                sh '''
                    npm ci
                    npm run build
                '''
            }
            
        }

        stage("Test"){
           parallel{
            stage('Unit Test') {
            agent {
                docker {
                    label "agent"
                    image 'node:18-alpine'
                    reuseNode true
                }
            }
            steps {
                sh '''
                    #test -f build/index.html
                    npm test
                '''
            }
            post{
                always{
                    junit 'test-results/junit.xml'
                    }
                }
            }
           
        

        stage('E2E') {
            agent {
                docker {
                    label "agent"
                    image 'mcr.microsoft.com/playwright:v1.39.0-jammy'
                    reuseNode true
                }
            }

            steps {
                sh '''
                    npm install serve
                    node_modules/.bin/serve -s build &
                    sleep 10
                    npx playwright test --reporter=html
                '''
                
                }
                post{
                    always{
                        publishHTML([allowMissing: false, alwaysLinkToLastBuild: false, icon: '', keepAll: false, reportDir: 'playwright-report', reportFiles: 'index.html', reportName: 'Playwright HTML Report', reportTitles: '', useWrapperFileDirectly: true])
                    }
                }
            }
        } 
    }

     stage("Deploy"){
            agent {
                docker {
                    image 'node:18-alpine'
                    reuseNode true
                    label 'agent'
                }
            }
            steps{
                sh '''
                npm install -g netlify-cli@20.1.1
                netlify --version
                
                '''
            }
        }
  }
       

    // post {
    //     always {
            //unable to execute the post stage
    //     }
    // }
}
