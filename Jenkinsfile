currentBuild.displayName = "First-git-pipline#" + currentBuild.number 
pipeline {
    agent any
    environment {
         DOCKER_TAG = getVersion()
    }

    stages {

        stage('Docker-build'){
            steps {
                sh 'docker build . -t khaledvb/ng:${DOCKER_TAG}'
            }
        }

        stage('Docker-push') {
            steps {
                withCredentials([string(credentialsId: 'khaledvbPWD', variable: 'dockerHubPwd')]) {
                    sh 'docker login -u khaledvb -p ${dockerHubPwd}'
                    sh 'docker push khaledvb/ng:${DOCKER_TAG}'
                }
            }
        }

        stage('Docker-clean') {
            steps {
                sh 'docker rm -f ngcontainer '
            }
        }

        stage('Docker-deplay') {
            steps {
                sh 'docker run --name ngcontainer -p 88:80 -d khaledvb/ng:${DOCKER_TAG}'
            }
        }
    }
}

def getVersion() {
     def v= sh returnStdout: true, script: 'git rev-parse --short HEAD'
     return v
}
