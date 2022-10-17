currentBuild.displayName = "First-pipline#" + currentBuild.number
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
                sh '''echo "hello from file"> /tmp/hellotest
                      cat /tmp/hellotest'''
            }
        }
    }
}
