
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
                        sh "docker build -t dockerhubcharan/docker_practice:$BUILD_NUMBER ."
                    }
                }
            }
        }
        
        stage('Push image') {
            steps {
                script {
                    docker.withRegistry('', DOCKERHUB_CREDENTIALS) {
                        sh "docker push dockerhubcharan/docker_practice:$BUILD_NUMBER"
                    }
                }
            }
        }
        
        stage('Pull image') {
            steps {
                script {
                    docker.withRegistry('', DOCKERHUB_CREDENTIALS) {
                        sh "docker pull dockerhubcharan/docker_practice:$BUILD_NUMBER"
                    }
                }
            }
        }
        
        stage('Run image') {
            steps {
                sh "docker run -d -p 443:80 dockerhubcharan/docker_practice:$BUILD_NUMBER"
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
