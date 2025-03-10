pipeline {
    agent any
    
    environment {
        ANSIBLE_DIR = 'ansible'
    }
    
    stages {
        stage('Checkout') {
            steps {
                // Clean workspace before build
                cleanWs()
                checkout scm
            }
        }
        
        stage('Python Test') {
            steps {
                sh 'python3 hello.py'
            }
        }
        
        stage('Calculator Test') {
            steps {
                dir('jenkins_demo1') {
                    sh 'python3 src/calculator.py'
                }
            }
        }
        
        stage('Ansible Setup') {
            steps {
                dir(ANSIBLE_DIR) {
                    // Run ansible playbook against localhost
                    sh 'ansible-playbook playbooks/setup.yml -i inventory.ini --limit local'
                }
            }
        }
    }
    
    post {
        success {
            echo 'Pipeline completed successfully!'
        }
        failure {
            echo 'Pipeline failed! Check the logs for details.'
        }
        always {
            echo 'Cleaning up workspace...'
            cleanWs()
        }
    }
}
