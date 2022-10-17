currentBuild.displayName = "First-git-pipline#" + currentBuild.number 
pipeline {
    agent any

    stages {
        stage('Docker-deplay') {
            steps {
                sh 'docker run --name mynginx -p 80:80 -d nginx'
            }
        }
    }
}
