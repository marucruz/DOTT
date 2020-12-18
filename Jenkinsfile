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
                sh 'docker build --tag ruby .'
            }
        }
        stage('Static Code Analysis') {
        environment {
            SCANNER_HOME = tool 'sonarcloudscanner'
            //ORGANIZATION = "marucruz"
            //PROJECT_NAME = "marucruz_DOTT"
            ORGANIZATION = credentials('org')
            PROJECT_NAME = credentials('projectN')
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
                catchError(buildResult: 'SUCCESS', stageResult: 'FAILURE') {
                    sh 'ruby tests.rb'
                }
            }
        }
        stage('Delete Existing Container') {
            steps {
                catchError(buildResult: 'SUCCESS', stageResult: 'FAILURE') {
                    sh 'docker stop rb'
                    sh 'docker rm rb'
                }
            }
        } 
        stage('Run Ruby Container') {
            steps {
                    sh 'docker run --publish 8000:8000 --detach --name rb ruby'
            }
        } 
    }
}
