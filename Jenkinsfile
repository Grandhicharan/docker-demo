pipeline {
    agent any
    environment {
        DOCKERHUB_CREDENTIALS = credentials('docker-hub-dockerhubcharan')
    }
    stages {
        stage('SCM Checkout') {
            steps {
                git 'https://github.com/BhaskarRao-D/DockerPipeline.git'
            }
        }

        stage('Build docker image') {
            steps {
                sh 'docker build -t dockerhubcharan/nginx1:8 .'
            }
        }

        stage('Login to DockerHub') {
            steps {
                sh 'echo $DOCKERHUB_CREDENTIALS_PSW | docker login -u $DOCKERHUB_CREDENTIALS_USR --password-stdin'
            }
        }

        stage('Push image') {
            steps {
                sh 'docker push dockerhubcharan/nginx1:8'
            }
        }

        stage('Pull image') {
            steps {
                sh 'docker pull dockerhubcharan/nginx1:8'
            }
        }

        stage('Run image') {
            steps {
                sh 'docker run -d -p 88:80 dockerhubcharan/nginx1:8'
            }
        }
    }

    post {
        always {
            sh 'docker logout'
        }
    }
}
