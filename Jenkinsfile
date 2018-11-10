

pipeline {
    agent any
    
    stages {
        stage('junit') {
            steps {
                sh "touch junit/test.xml"
                sh "false"
                archiveArtifacts artifacts: 'Mobile4/build/outputs/apk/**/*.apk'
            }
            
            post {
                always {
                    junit '**/*.xml'
                    
                }
            }
        }
    }
}
