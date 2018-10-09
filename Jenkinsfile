pipeline {
    agent any

    environment {
        APPLICATION_NAME = "my_example"
    }

    stages {
        stage('scm') {
            checkout([
              $class: 'GitSCM',
              branches: scm.branches,
              doGenerateSubmoduleConfigurations: false,
              extensions: scm.extensions + [[$class: 'SubmoduleOption', parentCredentials: true, recursiveSubmodules: true]],
              userRemoteConfigs: scm.userRemoteConfigs
            ])
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
