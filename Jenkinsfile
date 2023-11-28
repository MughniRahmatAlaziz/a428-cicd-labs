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
            }
        }
	stage('Manual Approval') {
            steps {
                input : 'Lanjutkan ke tahap Deploy? (Klik "Proceed" untuk melanjutkan Deploy)'
            }
        }
    stage('Deploy') { 
            steps {
                sh './jenkins/scripts/deliver.sh' 
                input message: 'Sudah selesai menggunakan React App? (Klik "Proceed" untuk mengakhiri)'
		        sh 'sleep 1m'
                sh './jenkins/scripts/kill.sh' 
            }
        }
    }
}
