pipeline {
    agent any

    environment {
        APPLICATION_NAME = "my_example"
    }

    stages {
        stage('verify mainline') {
            when {
                equals expected: false,
                actual: isMainlineBranch(scm)
            }

            steps {
                error('Aborting non-mainline branch')
            }

        }
    }
}

def isMainlineBranch(scm) {
    def mainlines = [ /^master$/, /^release\/.*$/, /feature\/live/ ]
    return null != scm.branches.find { branch ->
        mainlines.find { mainlineRegEx ->
            return branch ==~ mainlineRegEx
        }
    }
}