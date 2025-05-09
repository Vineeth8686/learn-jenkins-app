pipeline {
    agent any

    stages {
        stage("Echo") {
            agent {
                docker {
                    label 'agent' // Ensure correct label
                    image 'node:18-alpine'
                    reuseNode true
                }
            }
            steps {
                echo "This is from Echo Stage"
            }
        }

        stage("Test") {
            agent {
                docker {
                    label 'agent'
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

        stage("E2E") {
            agent {
                docker {
                    label "agent"
                    image 'mcr.microsoft.com/playwright:v1.39.0-jammy'
                }
            }
            steps {
                sh '''
                    npm install serve wait-on
                    npx serve -s build &
                    npx wait-on http://localhost:3000
                    npx playwright test --reporter=junit
                '''
            }
        }
    }

    post {
        always {
            junit '**/test-results.xml'
        }
    }
}