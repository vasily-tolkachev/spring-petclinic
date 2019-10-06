pipeline {
    agent any
     triggers {
        pollSCM '* * * * *'
     }
    stages {
        stage('Build') {
            steps {
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
                    sh 'mvn sonar:sonar'
                }
            }
         }

    }
    post {
        failure {
            emailext attachLog: true,
                body: '$DEFAULT_CONTENT',
                recipientProviders: [brokenBuildSuspects()],
                subject: '$DEFAULT_SUBJECT'
       }
    }
}
