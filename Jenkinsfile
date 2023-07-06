
pipeline {
    agent any 
    environment {
        DOCKERHUB_CREDENTIALS = credentials('docker-hub-dockerhubcharan')
    }
    stages { 
        stage('SCM Checkout') {
            steps {
                git branch: 'master', url: 'https://github.com/Grandhicharan/docker-demo.git'
            }
        }
        
        stage('Build docker image') {
            steps {  
                script {
                    docker.withRegistry('', DOCKERHUB_CREDENTIALS) {
                        sh "docker build -t dockerhubcharan/integration:$BUILD_NUMBER ."
                    }
                }
            }
        }
        
        stage('Push image') {
            steps {
                script {
                    docker.withRegistry('', DOCKERHUB_CREDENTIALS) {
                        sh "docker push dockerhubcharan/integration:$BUILD_NUMBER"
                    }
                }
            }
        }
        
        stage('Pull image') {
            steps {
                script {
                    docker.withRegistry('', DOCKERHUB_CREDENTIALS) {
                        sh "docker pull dockerhubcharan/integration:$BUILD_NUMBER"
                    }
                }
            }
        }
        
        stage('Run image') {
            steps {
                sh "docker run -d -p 443:80 dockerhubcharan/integration:$BUILD_NUMBER"
            }
        }
    }
    
    post {
        always {
            script {
                docker.withRegistry('', DOCKERHUB_CREDENTIALS) {
                    sh 'docker logout'
                }
            }
        }
    }
}
