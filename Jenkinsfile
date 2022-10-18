currentBuild.displayName = "First-git-pipline#" + currentBuild.number 
pipeline {
    agent any

    stages {

        stage('Docker-build'){
            steps {
                sh 'docker build . -t khaledvb/ng:latest'
            }
        }

        stage('Docker-push') {
            steps {
                withCredentials([string(credentialsId: 'khaledvbPWD', variable: 'dockerHubPwd')]) {
                    sh 'docker login -u khaledvb -p ${dockerHubPwd}'
                    sh 'docker push khaledvb/ng:latest'
                }
            }
        }

        stage('Docker-deplay') {
            steps {
                sh 'docker run --name mynginx -p 88:82 -d khaledvb/ng:latest'
            }
        }
    }
}
