pipeline {
    agent any
    stages {
        stage('Build Docker Image') {
            steps {
                sh 'docker build -t static-site:latest .'
            }
        }
        stage('Run Container') {
            steps {
                sh '''
                docker rm -f css-website || true
                docker run -d -p 80:80 --name css-website static-site:latest
                '''
            }
        }
    }
}
