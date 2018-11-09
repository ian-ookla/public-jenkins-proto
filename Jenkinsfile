

pipeline {
    agent any
    
    environment {
        APPLICATION_NAME = "my_example"
    }

    stages {
        stage('Build') {
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
}

/**
 * Returns true if any of the current branches are a mainline branch, otherwise false
 * @param branches list of current branches
 */
def isMainlineBranch() {
    def mainlines = [ /^master$/, /^release\/.*$/, /^feature\/live$/, /.*/ ]
    return null != scm.branches.find { branch ->
        mainlines.find { mainlineRegEx ->
            println "branch: ${branch} re: ${mainlineRegEx} match: ${branch ==~ mainlineRegEx}"
            return branch ==~ mainlineRegEx
        }
    }
}

enum BuildType {
    BUDDY, RELEASE, UNKNOWN
}

def getBuildType() {
    if (env.CHANGE_ID != null) {
        return BuildType.BUDDY
    } else if (isMainlineBranch()) {
        return BuildType.RELEASE
    } else {
        // TODO ookla iwh -- note force buddy here
        return BuildType.BUDDY
    }
}
