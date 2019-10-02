#!groovy

// SCM parameters
def commitId
def branchName

node {
    try {
        stage('Build') {
            steps {
                checkout scm
                bat 'mvn -B -DskipTests clean package'
            }
        }
    }
    catch (def e) {
        echo e.toString()
        currentBuild.result = 'FAILURE'
    }
}
