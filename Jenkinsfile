pipeline {
    agent any
    stages {
        stage('Versions') {
            steps {
                sh 'docker --version'
                sh 'git --version'
                sh 'ruby --version'
            }
        }
        stage('Build Ruby Image') {
            steps {
                dir('/var/lib/jenkins/workspace/devops_project_master/cidr_convert_api/ruby'){
                sh 'sudo docker build --tag ruby:1.0 .'
                }
            }
        }
        stage('Run Ruby Container') {
            steps {
                dir('/var/lib/jenkins/workspace/devops_project_master/cidr_convert_api/ruby'){
                sh 'sudo docker run --publish 8000:8000 --detach --name rb ruby:1.0'
                }
            }
        } 
        stage('Static Code Analysis') {
        environment {
            SCANNER_HOME = tool 'sonarcloudscanner'
            ORGANIZATION = "marucruz"
            PROJECT_NAME = "marucruz_DOTT"
         }
        steps {
         withSonarQubeEnv('sonarcloud') {
            sh '''$SCANNER_HOME/bin/sonar-scanner -Dsonar.organization=$ORGANIZATION \
            -Dsonar.java.binaries=build/classes/java/ \
            -Dsonar.projectKey=$PROJECT_NAME \
            -Dsonar.sources=.'''
             }
        }
        }
        stage('Testing') {
            steps {
                sh 'echo "Testing"'
                sh 'ruby tests.rb'
            }
        } 
    }
}
