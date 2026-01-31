node {
    def nodeImage = docker.image('node:16-buster-slim')
    
    stage('Checkout') {
        checkout scm [cite: 1]
    }
    nodeImage.inside('-p 3000:3000') {
        
        stage('Build') {
            sh 'npm install' [cite: 4]
        }

        stage('Test') {
            sh 'chmod +x ./jenkins/scripts/test.sh' [cite: 5]
            sh './jenkins/scripts/test.sh' [cite: 10]
        }

        stage('Manual Approval') {
            input message: 'Hasil Test sukses. Klik Proceed untuk lanjut Deploy ke Localhost?' [cite: 12]
        }

        stage('Deploy') {
            sh 'sleep 10'
            
            sh 'chmod +x ./jenkins/scripts/deliver.sh' [cite: 13]
            sh './jenkins/scripts/deliver.sh' [cite: 17]
            
            echo "Aplikasi berjalan di http://localhost:3000"
            sh 'sleep 120' 
        }
    }
}