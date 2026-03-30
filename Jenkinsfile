node {
    stage('Checkout') {
        checkout scm
    }

    docker.image('node:16-buster-slim').inside {
        stage('Build') {
            sh 'npm install'
            sh 'npm run build'
        }
        
        stage('Test') {
            sh 'chmod +x ./jenkins/scripts/test.sh'
            sh './jenkins/scripts/test.sh'
        }
    }

    stage('Manual Approval') {
        input message: 'Hasil tes aman? Lanjut ke tahap Deploy?', ok: 'Proceed'
    }

    docker.image('node:20-buster-slim').inside {
        stage('Deploy') {
            withCredentials([
                string(credentialsId: 'CF_PAGES_TOKEN', variable: 'CF_TOKEN'),
                string(credentialsId: 'CF_ACCOUNT_ID', variable: 'CF_ACCOUNT')
            ]) {
                echo "Mulai deploy ke Cloudflare Pages..."
                
                sh """
                    export CLOUDFLARE_API_TOKEN=${CF_TOKEN}
                    export CLOUDFLARE_ACCOUNT_ID=${CF_ACCOUNT}
                    npx wrangler pages deploy build --project-name=my-react-app
                """
            }

            echo "Aplikasi berhasil LIVE! Pipeline akan dijeda selama 1 menit..."

            sh 'sleep 60'
            
            echo "Waktu monitoring selesai. Eksekusi pipeline sukses!"
        }
    }
}