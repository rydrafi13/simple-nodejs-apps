pipeline {
    agent {
        node {
            label 'build-server'
            customWorkspace '/opt/jenkins/workspace/simple-apps'

        }
    }
    environment {
        REGISTRY = 'rydrafi'
        IMAGE = 'simple-nodejs-apps'

    }
    stages {
        stage('Build Apps') {
            steps {
                sh 'npm install'
            }
            
        }
        stage('Run Tests') {
            parallel {
                stage('Unit Testing & Coverage') {
                    steps {
                        sh '''npm test
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

        stage('Build Image') {
            steps {
                sh 'docker build -t ${IMAGE}:${BUILD_NUMBER} .'
            }   
        }

        stage('Tag & Push Image') {
            steps {
                sh '''docker tag ${IMAGE}:${BUILD_NUMBER} ${REGISTRY}/${IMAGE}:${BUILD_NUMBER}
                    docker push ${REGISTRY}/${IMAGE}:${BUILD_NUMBER}
                '''
            }   
        }
    }
}
