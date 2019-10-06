pipeline {
    agent any
    triggers {
        pollSCM '* * * * *'
    }
    stages {
        stage('Build') {
            steps {
                bat 'mvn -B -DskipTests clean package'
                versionNumberString = VersionNumber (versionNumberString: '1.0.${BUILDS_ALL_TIME}')
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
                    bat 'mvn sonar:sonar'
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
