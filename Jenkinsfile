pipeline {
    //Run agent on server 1
    agent {label 'server1-rifqi'}
    //Setup tools nodejs
    tools {nodejs 'nodejs'}
    //running CI/CD pipeline
    stages {
        stage('Checkout SCM') {
            steps {
                git branch: 'main', url: 'https://github.com/Rifqi-Achmad/simple-apps.git'
            }
        }
        stage('Build') {
            steps {
                sh '''cd apps
                npm install'''
            }
        }
        stage('Testing') {
            steps {
                sh '''cd apps
                npm test
                npm run test:coverage'''
            }
        }
        stage('Code Review') {
            steps {
                sh '''cd apps
                sonar-scanner \
                -Dsonar.projectKey=simple-apps \
                -Dsonar.sources=. \
                -Dsonar.host.url=http://10.23.10.102:9000 \
                -Dsonar.login=sqp_cec9f217a7f7156975ae47e1e79f250e485289ca'''
            }
        }
        stage('Deploy compose') {
            steps {
                sh '''
                docker compose build
                docker compose up -d
                '''
            }
        }
    }
}