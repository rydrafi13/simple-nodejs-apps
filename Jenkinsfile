pipeline {
    agent {
        node {
            label 'build-server'
            customWorkspace '/opt/jenkins/workspace/simple-apps'

        }
    }
    stages {
        stage('Build & Testing Apps') {
            steps {
                sh '''npm install
                      npm test
                      npm run test:coverage'''
            }
        }
    }
}
