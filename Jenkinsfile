pipeline {
    agent any
    stages {
        stage("SCM Checkout") {
            steps {
                checkout scm
            }
        }
        stage("Install Dependencies & Test") {
            steps {
                sh 'sudo yum install npm -y'
                sh 'npm install'
                sh 'npm test'
            }
        }
        stage("Build App") {
            steps {
                sh 'npm run build'
            }
        }
        stage("Build Docker Image") {
            steps {
                sh 'docker build -t my-node-app:1 .'
                sh 'docker tag my-node-app:1 cvreddy/vemarepo/my-node-app:1'
            }
        }
        stage("Push Docker Image") {
            steps {
                withCredentials([usernamePassword(credentialsId: 'docker-hub-password', usernameVariable: 'DOCKER_USER', passwordVariable: 'DOCKER_PASS')]) {
                    sh 'docker login -u cvreddy -p $DOCKER_PASS'
                    sh 'docker push cvreddy/vemarepo/my-node-app:1'
                }
            }
        }
    }
    post {
        always {
            cleanWs() // Clean workspace after build
        }
    }
}
