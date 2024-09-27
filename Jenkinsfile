pipeline {
    agent {
        docker { image 'node:16' }
    }
    stages {
        stage('Build') {
            steps {
                sh 'npm install --save'
            }
        }
        stage('Test') {
            steps {
                sh 'npm test'
            }
        }
        stage('Security Scan') {
            steps {
                withCredentials([string(credentialsId: 'snyk-token', variable: 'SNYK_TOKEN')]) {
                    // Install Snyk locally instead of globally
                    sh 'npm install snyk'
                    // Run Snyk using the local installation
                    sh './node_modules/.bin/snyk test'
                }
            }
        }
        stage('Deploy') {
            steps {
                echo 'Deploying...'
            }
        }
    }
}
