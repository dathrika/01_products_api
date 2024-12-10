pipeline {
    agent any
    tools {
        maven 'Maven-3.9.9'
    }
    stages {
        stage('Git clone') {
            steps {
                git branch: 'main', url: 'https://github.com/dathrika/01_products_api.git'
            }
        }
        stage('Maven Build') {
            steps {
                sh 'mvn clean package'
            }
        }
        stage('Docker Build') {
            steps {
                sh 'docker build -t sagard1531/products .'
            }
        }
        stage('Docker login') {
            steps {
                withCredentials([string(credentialsId: 'Docker_login_password', variable: 'DOCKER_LOGIN_PASSWORD')]) {
                    sh 'docker login -u sagard1531 -p ${DOCKER_LOGIN_PASSWORD}'
                }
            }
        }
        stage('Dockerhub push') {
            steps {
                sh 'docker push sagard1531/products .'
            }
        }
        stage('k8s deployment'){
            steps{
             sh 'kubectl apply -f Deployment.yml'
            }
        }        
    }
}
