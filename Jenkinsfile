pipeline {
    agent none
    environment{
        NETLIFY_SITE_ID = "8b52e730-7446-40f4-8aaf-4490be509d0f"
        NETLIFY_AUTH_TOKEN = credentials('netlify-token')
    }
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

    //     stage("Test"){
    //        parallel{
    //     stage('Unit Test') {
    //         agent {
    //             docker {
    //                 label "agent"
    //                 image 'node:18-alpine'
    //                 reuseNode true
    //             }
    //         }
    //         steps {
    //             sh '''
    //                 #test -f build/index.html
    //                 npm test
    //             '''
    //         }
    //         post{
    //             always{
    //                 junit 'test-results/junit.xml'
    //                 }
    //             }
    //         }
           
        

    //     stage('E2E') {
    //         agent {
    //             docker {
    //                 label "agent"
    //                 image 'mcr.microsoft.com/playwright:v1.39.0-jammy'
    //                 reuseNode true
    //             }
    //         }

    //         steps {
    //             sh '''
    //                 npm install serve
    //                 node_modules/.bin/serve -s build &
    //                 sleep 10
    //                 npx playwright test --reporter=html
    //             '''
                
    //             }
    //             post{
    //                 always{
    //                     publishHTML([allowMissing: false, alwaysLinkToLastBuild: false, icon: '', keepAll: false, reportDir: 'playwright-report', reportFiles: 'index.html', reportName: 'Playwright HTML Report', reportTitles: '', useWrapperFileDirectly: true])
    //                 }
    //             }
    //         }
    //     } 
    // }

    //  stage("Deploy"){
    //         agent {
    //             docker {
    //                 image 'node:18-alpine'
    //                 reuseNode true
    //                 label 'agent'
    //             }
    //         }
    //         steps{
    //             sh '''
    //             npm install netlify-cli
    //             node_modules/.bin/netlify --version
    //             echo "Deploying to Production Site ID:$NETLIFY_SITE_ID"
    //             node_modules/.bin/netlify status
    //             node_modules/.bin/netlify deploy --dir=build --prod
    //             '''
    //         }
    //     }
  }
       

    post {
       always{
         node("agent"){  
                withDockerContainer('node:18-alpine') {              
                    sh "npm --version"
             }
         }
       }
    }
}

