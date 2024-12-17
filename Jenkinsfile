pipeline {
    agent any

    stages {
        // This is a single line comment
        /*
        this is a 
        multiline comment
        */
        stage ('Build') {
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
                        npm ci
                        npm run build
                        ls -la
                    '''
                }
        }
        stage ('Test') {
            agent {
                docker {
                    image 'node:18-alpine'
                    reuseNode true
                }
            }
            steps {
                sh '''
                    test -f build/index.html
                    npm test
                '''
            }
        }
                
    }
    post {
        always {
            junit 'test-results/junit.xml'
        }
    }
}


