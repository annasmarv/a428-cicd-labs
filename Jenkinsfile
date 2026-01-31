node {
    // Stage 1: Ambil kode dari GitHub
    stage('Checkout') {
        checkout scm
    }

    // Stage 2: Proses Build
    stage('Build') {
        // Sesuaikan perintah sh dengan kebutuhan React App kamu
        // Contoh jika menggunakan Docker untuk build:
        sh 'docker build -t my-react-app .'
    }

    // Stage 3: Proses Test
    stage('Test') {
        // Contoh menjalankan test di dalam container
        sh 'echo "Running tests..." '
        // sh 'docker run my-react-app npm test'
    }
}