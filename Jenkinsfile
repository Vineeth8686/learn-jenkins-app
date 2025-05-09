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
                    ls -la
                    node --version
                    npm --version
                    npm ci
                    npm run build
                    ls -la
                '''
            }
        }
    

        stage('Test') {
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
                    npx playwright test
                '''
            }
        }
    }

    // post {
    //     always {
    //         junit 'jest-results/junit.xml'
    //     }
    // }
}
