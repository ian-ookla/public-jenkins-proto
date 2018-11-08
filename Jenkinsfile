pipeline {
    agent any

    environment {
        APPLICATION_NAME = "my_example"
    }

    stages {
        // stage('scm') {
        //     [
        //         $class: 'GitSCM',
        //         branches: [[name: '**']], 
        //         doGenerateSubmoduleConfigurations: false, 
        //         extensions: [
        //             [
        //                 $class: 'SubmoduleOption', 
        //                 disableSubmodules: false, 
        //                 parentCredentials: true, 
        //                 recursiveSubmodules: true, 
        //                 reference: '', 
        //                 trackingSubmodules: false
        //             ]
        //         ],
        //         submoduleCfg: [],
        //         userRemoteConfigs:
        //         [
        //             [
        //                 credentialsId: '944fee11-7d97-4388-9802-4bc5304df0cd',
        //                 url: 'git@github.com:ian-ookla/public-jenkins-proto.git']
        //             ]
        //         ]
        // }
        stage('build_buddy') {
            when {
                equals expected: BuildType.BUDDY, actual: getBuildType()
            }

            steps {
                echo "Building buddy"
            }
        }
        
        stage('build_release') {
            when {
                equals expected: BuildType.RELEASE, actual: getBuildType()
            }
            
            steps {
                echo "Building release"
            }
        }
    }
}

enum BuildType {
    BUDDY, RELEASE
}

def getBuildType() {
    if (env.CHANGE_ID == null) {
        return BuildType.RELEASE
    } else {
        return BuildType.BUDDY
    }
}
