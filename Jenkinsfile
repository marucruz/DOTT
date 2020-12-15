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
                sh 'sudo docker build --tag ruby:1.0 .'
                sh 'sudo docker run --publish 8000:8000 --detach --name rb ruby:1.0'
                }
            }
        }
        
    }
}
