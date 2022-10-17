currentBuild.displayName = "First-git-pipline#" + currentBuild.number 
pipeline {
    agent any

    stages {
        stage('Docker-deplay') {
            steps {
                sh 'docker run --name mynginx -p 88:80 -d nginx'
            }
        }
        stage('Docker-tag') {
            steps {
                sh 'docker tag nginx:latest khaledvb/ng:latest'
            }
        }
        stage('Docker-push') {
            steps {
                withCredentials([string(credentialsId: 'khaledvbPWD', variable: 'dockerHubPwd')]) {
                    sh 'docker login -u khaledvb -p ${dockerHubPwd}'
                    sh 'docker push nginx:latest khaledvb/ng:latest'
                }
            }
        }
    }
}
