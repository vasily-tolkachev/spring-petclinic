pipeline {
    agent any
    triggers {
        pollSCM 'H/2 * * * *'
    }
    environment {
        versionNumberString = VersionNumber projectStartDate: '',
            versionNumberString: '${BUILDS_THIS_YEAR}',
            versionPrefix: '1.0.',
            worstResultForIncrement: 'SUCCESS'
    }
    stages {
        stage('Build') {
            steps {
                echo 'smth1'
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

        stage("SonarQube analysis") {
            agent any
            steps {
                withSonarQubeEnv('sonar') {
                    bat 'mvn sonar:sonar1'
                }
            }
         }
    }
    post {
        failure {
            emailext attachLog: true,
                body: '$DEFAULT_CONTENT',
                recipientProviders: [culprits()],
                subject: '$DEFAULT_SUBJECT'
        }
    }
}
