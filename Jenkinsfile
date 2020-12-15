pipeline {
    agent any
    stages {
        stage('Versions') {
            steps {
                sh 'docker --version'
                sh 'git --version'
            }
        }
        
        stage('Build image') {
            steps {
                dir('/var/lib/jenkins/workspace/devops_project_master/cidr_convert_api/ruby'){
                sh 'sudo docker build --tag ruby:1.0 .'
                }
            }
        }
        stage('Run container') {
            steps {
                dir('/var/lib/jenkins/workspace/devops_project_master/cidr_convert_api/ruby'){
                sh 'sudo docker run --publish 8000:8000 --detach --name rb ruby:1.0'
                }
            }
        }        
    }
}
