pipeline{
    agent {
        docker{
            label "slave"
            image "node:18-alpine"
            reuseNode true
        }
    }

    stages{
        stage("Git Checkout"){
            steps{
                sh '''
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