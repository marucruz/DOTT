pipeline {
        agent any
        stages {
        stage('Build Ruby Container') {
                steps {
                        sh 'echo "Step One"'
                        return docker.build("ruby", "-f https://github.com/marucruz/DOTT.git .")
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
