pipeline {
    agent {
        node {
            label 'build-server'
            customWorkspace '/opt/jenkins/workspace/simple-apps'

        }
    }
    environment {
        DB_NAME = 'training'
        DB_HOST = '10.23.1.1'
        DB_USER = 'peserta'
        DB_PASS = 'password'
        APP_PORT = '3000'

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
