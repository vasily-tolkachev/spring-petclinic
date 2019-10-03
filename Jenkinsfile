#!groovy

// SCM parameters
def commitId
def branchName

node {
    try {
        stage('Build') {

               // checkout scm
               // bat 'mvn -B -DskipTests clean package'
            mail bcc: '',
                 body: 'Test jenkins email notification',
                 cc: '', from: '', replyTo: '',
                 subject: 'Test jenkins email notification',
                 to: 'vasilii_tolkachev@epam.com'
        }
    }
    catch (def e) {
        echo e.toString()

        //send email
        currentBuild.result = 'FAILURE'
    }
}
