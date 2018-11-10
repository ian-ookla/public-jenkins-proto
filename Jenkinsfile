

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
                    archiveArtifacts artifacts 'Mobile4/build/outputs/apk/**/*.apk'
                }
            }
        }
    }
}
