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
            input {
                message "Lanjutkan ke tahap Deploy?"
            }
            steps {
                echo "Ready to deployment"
            }
        }
        stage('Deploy') { 
            steps {
                sh './jenkins/scripts/deliver.sh' 
                echo 'Aplikasi berhasil di-deploy. Menjeda eksekusi pipeline selama 1 menit...'
                sleep time: 60, unit: 'SECONDS'
                sh './jenkins/scripts/kill.sh' 
            }
        }
    }
}