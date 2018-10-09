pipeline {
    agent any

    environment {
        APPLICATION_NAME = "my_example"
    }

    stages {
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
                    submoduleCfg: [],
                    userRemoteConfigs:
                    [
                        [
                            credentialsId: '944fee11-7d97-4388-9802-4bc5304df0cd',
                            url: 'git@github.com:ian-ookla/public-jenkins-proto.git']
                        ]
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
