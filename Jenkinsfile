

pipeline {
    agent any
    
    stages {
        stage('junit') {
            steps {
                sh "touch junit/test.xml"
                sh "false"
                
            }
            
            post {
                always {
                    junit '**/*.xml'
                    recordJenkinsArtifacts()
                    
                }
            }
        }
    }
}

def recordJenkinsArtifacts() {
    archiveArtifacts artifacts: 'Mobile4/build/outputs/apk/**/*.apk'
}
