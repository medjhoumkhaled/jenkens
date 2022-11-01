currentBuild.displayName = "First-git-pipline#" + currentBuild.number 
pipeline {
    agent any
    environment {
         DOCKER_TAG = getVersion()
    }

    stages {
        stage('Data settings'){
            steps {
                sh 'chmod +x updateIndexVersion.sh'
                sh './updateIndexVersion.sh ${DOCKER_TAG} index.html'
                sh './updateIndexVersion.sh ${DOCKER_TAG} jktest.html'

            }
        }
        
        stage('Deploy in remote eu webserver'){
            steps {
                withCredentials([sshUserPrivateKey(credentialsId: 'com-server', keyFileVariable: 'EU_prevatefile')]) {
                    sh 'scp -oStrictHostKeyChecking=no -i ${EU_prevatefile} jktest.html root@login.cloutik.eu:/root/'
                }
                
                
                
            }
        }

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

        stage('Docker-deploy') {
            steps {
                sh 'docker run --name ngcontainer -p 88:80 -d khaledvb/ng:${DOCKER_TAG}'
            }
        }
        
        stage('Deploy in local webserver'){
            steps {
                sh 'cp jktest.html /var/www/html/cloutik/'
            }
        }
               
        stage('Deploy in remote webserver'){
            steps {
                withCredentials([sshUserPrivateKey(credentialsId: 'com-server', keyFileVariable: 'EU_prevatefile')]) {
                    sh 'scp -oStrictHostKeyChecking=no -i ${EU_prevatefile} jktest.html root@login.cloutik.eu:/root/'
                }
                
                
                
            }
        }
    }
}

def getVersion() {
     def v= sh returnStdout: true, script: 'git rev-parse --short HEAD'
     return v
}
