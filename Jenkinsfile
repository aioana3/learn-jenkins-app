pipeline {
    agent any

    stages {
        stage('Build') {
            agent {
                docker {
                    image 'node:18-alpine'
                    reuseNode true
                }
            }
            steps {
                sh ''' 
                    ls -la
                    node --version
                    npm --version
                    echo 'Create node_modules folder'
                    npm ci
                    echo 'Create Build folder'
                    npm run build
                    ls -la
                '''
            }
        }
    }
}