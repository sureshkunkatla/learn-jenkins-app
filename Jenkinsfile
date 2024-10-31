pipeline {
    agent any

    stages {
        stage('Build') {
            agent{
                docker{
                    image 'node:18-alpine'
                    reuseNode true
                }
            }
            steps {
                sh'''
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
            steps {
                sh'''
                    echo "Test stage"
                    if test -f "build/index.html";then
                        echo "index.html file exists"
                    else
                        echo "index.html file does not exists"
                        exit 1
                    fi
                '''
                sh 'npm test'
            }
        }
    }
}
