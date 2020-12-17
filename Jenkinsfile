pipeline {
    agent any
    stages {
        script {
            env.WORKSPACE = $WORKSPACE/cidr_convert_api/ruby
        }
        stage('Versions') {
            steps {
                sh 'docker --version'
                sh 'git --version'
                sh 'ruby --version'
                sh 'echo $WORKSPACE'
            }
        }
        stage('Testing') {
            steps {
                dir('$WORKSPACE/cidr_convert_api/ruby'){
                    sh 'echo "Testing"'
                catchError(buildResult: 'SUCCESS', stageResult: 'FAILURE') {
                    sh 'ruby tests.rb'
                }
                }
            }
        }
        stage('Build Ruby Image') {
            agent {
            // Equivalent to "docker build -f Dockerfile.build --build-arg version=1.0.2 ./build/
            dockerfile {
                filename 'Dockerfile'
                dir 'cidr_convert_api/ruby'
                label 'my-defined-label'
                additionalBuildArgs  '--build-arg version=1.0.2'
                args '-v /tmp:/tmp'
             }
            }
            steps {
                dir('/cidr_convert_api/ruby'){
                sh 'docker build --tag ruby:1.0 .'
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
                dir('/cidr_convert_api/ruby'){
                    sh 'docker run --publish 8000:8000 --detach --name rb ruby:1.0'
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
    }
}
