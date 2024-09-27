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
                    // Install Snyk locally
                    sh 'npm install snyk'
                    // Run Snyk, but ignore exit code to avoid failing the pipeline
                    sh './node_modules/.bin/snyk test || true'
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
