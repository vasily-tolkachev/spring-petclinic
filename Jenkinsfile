#!groovy

// SCM parameters
def commitId
def branchName

@Library('jenkins-pipeline-shared-lib-sample')_

node {
    try {
        stage('Collect info') {

            printBuildinfo {
                name = "Sample Name"
            }
            checkStatus()
        }
    }
    catch (def e) {
        echo e.toString()
        currentBuild.result = 'FAILURE'
    }
}
