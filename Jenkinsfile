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
              {
                            env.ForEmailPlugin = env.WORKSPACE
                            emailext attachmentsPattern: 'TestResults\\*.trx',
                            body: '''${SCRIPT, template="groovy_html.template"}''',
                            subject: currentBuild.currentResult + " : " + env.JOB_NAME,
                            to: 'vasilii_tolkachev@epam.com'
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
