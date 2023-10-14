pipeline {
    agent {
        docker {
            image 'node:16-buster-slim'
            args '-p 3000:3000'
        }
    }
    stages {
        stage('Build') {
            steps {
                sh 'npm install'
            }
        }
        stage('Test') {
            steps {
                sh './jenkins/scripts/test.sh'
                input message: 'Lanjut ke tahap deploy? (Klik "Proceed" untuk melanjutkan)'
            }
        }
        stage('Manual Approval') {
            steps {
                input message: 'Lanjut ke tahap deploy? (Klik "Proceed" untuk melanjutkan)'
            }
        }
        stage('Deploy') { 
            steps {
                sh './jenkins/scripts/deliver.sh' 
                sh 'sleep 1m'
                sh './jenkins/scripts/kill.sh' 
            }
        }
    }
}