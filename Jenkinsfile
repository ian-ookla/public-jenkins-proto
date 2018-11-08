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
        
        stage('Validate build type') {
            when {
                equals expected: BuildType.UNKNOWN, actual: getBuildType()
            }

            steps {
                error('Failing on unknown build type')
            }
        }
        
        
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

/**
 * Returns true if any of the current branches are a mainline branch, otherwise false
 * @param branches list of current branches
 */
def isMainlineBranch(branches) {
    def mainlines = [ /^master$/, /^release\/.*$/, /^feature\/live$/, /.*/ ]
    return null != branches.find { branch ->
        mainlines.find { mainlineRegEx ->
            println "branch: ${branch} re: ${mainlineRegEx} match: ${branch ==~ mainlineRegEx}"
            return branch ==~ mainlineRegEx
        }
    }
}

enum BuildType {
    BUDDY, RELEASE, UNKNOWN
}

println "THIS ${this}"

def getBuildType() {
    if (env.CHANGE_ID != null) {
        return BuildType.BUDDY
    } else if (isMainlineBranch(scm.branches)) {
        return BuildType.RELEASE
    } else {
        return BuildType.UNKNOWN
    }
}
