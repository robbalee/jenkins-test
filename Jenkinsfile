pipeline {
    agent any
    stages {
        stage('build') {
            steps {
                sh 'echo "Hello, World!"'
                sh 'echo "testing jenkins"'
            }
        }
        
        stage('Check Python') {
            steps {
                sh 'python3 --version'
                sh 'pip3 --version'
            }
        }
    }
}
