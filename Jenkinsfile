pipeline {
    agent any
    
    stages {
        stage('Setup') {
            steps {
                dir('jenkins_demo1') {  // Change to jenkins_demo1 directory
                    sh 'python3 -m pip install --upgrade pip'
                    sh 'pip3 install -r requirements.txt'
                }
            }
        }
        
        stage('Lint') {
            steps {
                dir('jenkins_demo1') {
                    sh 'pylint src/ tests/ || true'
                }
            }
        }
        
        stage('Test') {
            steps {
                dir('jenkins_demo1') {
                    sh 'python3 -m pytest tests/ --junitxml=test-results/junit.xml'
                    sh 'coverage run -m pytest tests/'
                    sh 'coverage report'
                    sh 'coverage html -d coverage-reports'
                }
            }
        }
    }
    
    post {
        always {
            dir('jenkins_demo1') {
                junit 'test-results/*.xml'
                publishHTML([
                    allowMissing: false,
                    alwaysLinkToLastBuild: true,
                    keepAll: true,
                    reportDir: 'coverage-reports',
                    reportFiles: 'index.html',
                    reportName: 'Coverage Report'
                ])
            }
        }
    }
}
