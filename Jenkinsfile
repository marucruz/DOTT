pipeline {
        agent { dockerfile true }
        stages {
        stage('Docker version') {
                steps {
                        sh 'docker version'
                }
        }
        stage('Build Ruby Container') {
                steps {
                        sh 'echo "Step One"'
                }
        }
        stage('Code Analysis') { 
                steps {
                        sh 'echo "Analyzing"'
                        }
                }
        stage('Tests') {
                steps {
                        sh 'echo "Testing"'
                        }
                }
        }
}
