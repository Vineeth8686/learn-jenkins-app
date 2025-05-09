pipeline{
    agent {
        docker{
            label "slave"
            image "node:18-alpine"
            reuseNode true
        }
    }

    stages{
        //This is a Build Stage
        stage("Build"){
            steps{
                sh '''
                    npm ci
                    npm run build
                '''
                
            }
        }
        stage("Test"){
            //This is a Test Stage
            steps{
                echo "Test Stage"
                sh '''
                    test -f build/index.html && echo "index.html exists" || echo "index.html not found"
                    npm test
                '''
                
            }    
        }
        stage("E2E"){
            agent{
                docker{
                    label "slave"
                    image "mcr.microsoft.com/playwright:v1.39.0-jammy"
                    reuseNode true
                    args '-u root:root'
                }
            }
            steps{
                sh'''
                npm install serve
                node_modules/.bin/serve -s build &
                sleep 10
                npx playwright test
                '''
            }
        }
    }
    post{
        always{
            junit stdioRetention: 'ALL', testResults: '**/test-results/*.xml'
        }
    }
}
