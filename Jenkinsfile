pipeline {
    agent any

    environment {
        APPLICATION_NAME = "my_example"
    }

    stages {

        when { equals expected: true, actual: isMainlineBranch() }

        stage('scm') {
            steps {
                checkout([
                    $class: 'GitSCM',
                    branches: scm.branches, 
                    doGenerateSubmoduleConfigurations: false, 
                    extensions: [
                        [
                            $class: 'SubmoduleOption', 
                            disableSubmodules: false, 
                            parentCredentials: true, 
                            recursiveSubmodules: true, 
                            reference: '', 
                            trackingSubmodules: false
                        ]
                    ],
                    userRemoteConfigs: scm.userRemoteConfigs
                ])
            }
        }
        stage('build') {
            steps {
                echo "Building"
            }
        }
        
        stage('test') {
            steps {
                echo "Testing"
            }
        }
    }
}

def isMainlineBranch() {
    true
}
