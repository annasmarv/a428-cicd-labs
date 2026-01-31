node {
    def nodeImage = docker.image('node:16-buster-slim')
    
    stage('Checkout') {
        checkout scm
    }

    nodeImage.inside('-p 3000:3000') {
        
        stage('Build') {
            sh 'npm install'
        }

        stage('Test') {
            sh 'chmod +x ./jenkins/scripts/test.sh'
            sh './jenkins/scripts/test.sh'
        }

        stage('Manual Approval') {
            input message: 'Hasil Test sukses. Lanjut Deploy?'
        }

        stage('Deploy') {
            sh 'sleep 10'
            sh 'chmod +x ./jenkins/scripts/deliver.sh'
            sh './jenkins/scripts/deliver.sh'
            
            echo 'Aplikasi berjalan di http://localhost:3000'
            // Memberikan waktu 120 detik untuk screenshot sebelum container mati
            sh 'sleep 120'
        }
    }
}