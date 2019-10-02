#!groovy

// SCM parameters
def commitId
def branchName

node {
    try {
        stage('Collect info') {
            checkout scm


            bat 'mvn -v'
        }
    }
    catch (def e) {
        echo e.toString()
        currentBuild.result = 'FAILURE'
    }
}
