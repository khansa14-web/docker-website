pipeline {
    agent any

    tools {
        jdk 'jdk17'
    }

    environment {
        SONAR_SCANNER_HOME = tool 'sonar-scanner'
    }

    stages {

        stage('Checkout Code') {
            steps {
                git 'https://github.com/khansa14-web/docker-website.git'
            }
        }

        stage('SonarQube Analysis') {
            steps {
                withSonarQubeEnv('SonarQube') {
                    sh '''
                        $SONAR_SCANNER_HOME/bin/sonar-scanner \
                        -Dsonar.projectKey=docker-website \
                        -Dsonar.sources=.
                    '''
                }
            }
        }

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
