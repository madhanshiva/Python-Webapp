pipeline {
    agent any

    stages {
        stage('Git Checkout') {
            steps {
                git branch: 'main', changelog: false, poll: false, url: 'https://github.com/madhanshiva/Python-Webapp.git'
            }
        }
        stage('Docker Build') {
            steps {
                sh 'make image'
            }
        }
        stage('Docker Push') {
            steps {
                withDockerRegistry([credentialsId: '961f6ec3-fa2a-4821-a99d-cde5c51adcc2', url: 'https://index.docker.io/v1/']) {
                    sh 'make push'
                }
            }
        }
        stage('Docker deploy') {
            steps {
                withDockerRegistry([credentialsId: '961f6ec3-fa2a-4821-a99d-cde5c51adcc2', url: 'https://index.docker.io/v1/']) {
                    sh 'docker images'
                    sh 'docker run -d --rm -it -p 5000:5000 mvmadhan/python-webapp:latest'
                }
            }
        }
    }
}

