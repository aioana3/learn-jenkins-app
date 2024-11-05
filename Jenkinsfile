pipeline {
    agent any

    stages {
        /*
        stage('Build') {
            agent{
                docker{
                    image 'node:18-alpine'
                    reuseNode true
                }
            }
            steps {
                sh '''
                ls -la
                node --version
                npm ---version
                npm ci
                npm run build
                ls -la 
                '''
            }
        }
        */
        
        stage('Test') {
            post {
                always {
                    junit'yest-results/junit.xml'
                }
            }
            agent{
                docker{
                    image 'node:18-alpine'
                    reuseNode true
                }
            }
            steps{            
                sh''' 
                    test -f build/index.html
                    npm test
                '''
            }
        }
        

stage('E2E') {
            agent{
                docker{
                    image 'mcr.microsoft.com/playwright:v1.48.1-noble'
                    reuseNode true
                    args '-u root:root'
                }
            }
            steps{            
                sh''' 
                    npm install -g serve
                    serve -s build &
                    sleep 15
                    npx playwright test --reporter=html                  
                '''
            }
        }
    }


}
