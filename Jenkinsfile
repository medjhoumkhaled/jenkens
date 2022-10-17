currentBuild.displayName = "First-git-pipline#" + currentBuild.number 
pipeline {
    agent any

    stages {
        stage('Hello') {
            steps {
                echo 'Hello World'
            }
        }
        stage('Hello from file') {
            steps {
                sh 'echo "hello from git file"> /tmp/githellotest'
            }
        }
    }
}
