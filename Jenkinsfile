pipeline {
    agent any
    stages {
        stage('Docker Version') {
            steps {
                sh 'docker --version'
            }
        }
        
        stage('Git Version') {
            steps {
                sh 'git --version'
                sh 'cd /'
                sh 'pwd'
                sh 'ls'
            }
        }
        
    }
}
