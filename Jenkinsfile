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
                sh 'pwd'
                dir('/var/lib/jenkins/workspace/devops_project_master/cidr_convert_api/ruby'){
                sh 'pwd'
                sh 'ls'
                }
                sh 'pwd'
                sh 'ls'
            }
        }
        
    }
}
