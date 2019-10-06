pipeline {
    agent any
     triggers {
        pollSCM '* * * * *'
     }
    stages {
/*
        stage('Email') {
            steps {
                emailext body: 'dsvdsvs', subject: 'Test ', to: 'vasilii_tolkachev@epam.com'
            }
        }

*/

        stage('Build') {
            steps {

                        echo 'This will always run'
                bat 'mvn -B -DskipTests clean package'
            }
        }


        stage('Test') {
            steps {
                bat 'mvn test'
            }
            post {
                always {
                    junit 'target/surefire-reports/*.xml'
                }
            }
        }

        stage('Email') {

            steps {
            emailext attachLog: true, body: '', recipientProviders: [brokenBuildSuspects()], subject: 'Build result'
              /*    echo GIT_COMMITTER_EMAIL
                emailext body: '''${SCRIPT, template="jenkins-matrix-email-html.template"}''',
                                subject: "[Jenkins] REPORT",
                                to: "vasilii_tolkachev@epam.com"
                                */
            }
        }
                    /*
        stage("SonarQube analysis") {
            agent any
            steps {
                withSonarQubeEnv('sonar') {
                    bat 'mvn sonar:sonar'
                }
            }
         }
         */
    }
    post {
        always {
            echo 'This will always run'
        }
    }
}
