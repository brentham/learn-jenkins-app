pipeline {
    agent any

    stages {
        stage('w/ docker') {
            agent {
                docker {
                    image 'node:18-alpine'
                    reuseNode true
                }
            }
            steps {
                sh '''
                    ls -la
                    npm ci
                    npm run build
                    ls -la
                '''
            }
        }

        stage('Test') {
            steps{
                echo 'Test Stage'
            }
        }
    }
}
