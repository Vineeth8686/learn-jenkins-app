pipeline{
    agent {
        docker{
            label "slave"
            image "node:18-alpine"
            reuseNode true
        }
    }

    stages{
        stage("Build"){
            steps{
                sh '''
                    npm ci
                    npm run build
                '''
                
            }
        }
        stage("Test"){
            steps{
                echo "Test Stage"
                // sh '''
                    
                // '''
                
            }    
        }
    }
}
