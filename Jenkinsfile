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
            input message: 'Hasil tes sudah oke? Lanjutkan ke tahap Deploy?'
        }

        stage('Deploy') {
            sh 'sleep 10'
            
            echo "Menjalankan aplikasi di server lokal..."
            sh 'chmod +x ./jenkins/scripts/deliver.sh'
            sh './jenkins/scripts/deliver.sh'
            
            echo "Aplikasi berhasil berjalan!"
        }
    } 
} 