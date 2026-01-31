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
    }

    stage('Manual Approval') {
        input message: 'Hasil tes sudah oke? Klik Proceed untuk menjalankan aplikasi secara lokal.'
    }

    stage('Deploy') {
        sh 'sleep 10'
        sh 'chmod +x ./jenkins/scripts/deliver.sh'
        
        // Jalankan aplikasi
        sh './jenkins/scripts/deliver.sh'
        
        // KRITERIA 4: Gunakan input di sini untuk menahan proses agar tidak mati
        input message: 'Aplikasi sudah jalan di http://localhost:3000. Klik Proceed jika ingin mematikan aplikasi.'
        
        // (Opsional) Jalankan script kill jika ada
        // sh './jenkins/scripts/kill.sh'
    }
}