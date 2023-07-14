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
        stage('Code Review') {
            steps {
                sh '''sonar-scanner \
                    -Dsonar.projectKey=simple-apps-nodejs \
                    -Dsonar.sources=. \
                    -Dsonar.host.url=http://10.23.1.40:9000 \
                    -Dsonar.login=sqp_7cc14798a06b72d5bf41ed60332c81238ef17910'''
            }   
        }
    }
}
