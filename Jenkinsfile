node {
    // Definisi image yang akan digunakan
    def nodeImage = docker.image('node:16-buster-slim')

    stage('Checkout') {
        // Mengambil kode dari GitHub
        checkout scm
    }

    // Menjalankan perintah di dalam container
    nodeImage.inside('-p 3000:3000') {
        
        stage('Build') {
            sh 'npm install'
        }

        stage('Test') {
            // Memastikan file script memiliki izin eksekusi
            sh 'chmod +x ./jenkins/scripts/test.sh'
            sh './jenkins/scripts/test.sh'
        }
    }
}