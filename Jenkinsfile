pipeline {
    agent any

    environment {
        IMAGE_NAME = 'pranavc07/2135_mini_finance'
        DOCKER_HUB_CREDENTIALS = credentials('docker-hub-cred')
    }

    stages {
        stage('Clone Repository') {
            steps {
                git 'https://github.com/Pranavmc/template=site.git'
            }
        }

        stage('Build Docker Image') {
            steps {
                script {
                    docker.build("${nginx}")
                }
            }
        }

        stage('Run Container') {
            steps {
                sh "docker run -d -p 8080:80 ${nginx}"
            }
        }

        stage('Push to Docker Hub') {
            steps {
                script {
                    docker.withRegistry('https://index.docker.io/v1/', DOCKER_HUB_CREDENTIALS) {
                        docker.image("${nginx}").push('latest')
                    }
                }
            }
        }
    }
}
