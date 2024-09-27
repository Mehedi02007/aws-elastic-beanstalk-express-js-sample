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
                    // Install Snyk using the --unsafe-perm flag to avoid permission issues
                    sh 'npm install -g snyk --unsafe-perm'
                    sh 'snyk test'
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
