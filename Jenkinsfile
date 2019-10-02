#!groovy

// SCM parameters
def commitId
def branchName

node {
    try {
        stage('Collect info') {
            checkout scm

            commitId = gitUtils.getCommitId()
            branchName = gitUtils.getBranchName()
            echo "${branchName}"
        }
    }
    catch (def e) {
        echo e.toString()
        currentBuild.result = 'FAILURE'
    }
}
