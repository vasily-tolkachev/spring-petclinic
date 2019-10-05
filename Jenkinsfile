pipeline {
    agent any
    stages {
    /*
        stage('Test') {
            steps {
                emailext body: 'dsvdsvs', subject: 'Test ', to: 'vasilii_tolkachev@epam.com'
            }
        }
        */

        stage("build & SonarQube analysis") {
                    agent any
                    steps {
                      withSonarQubeEnv('My SonarQube Server') {
                        sh 'mvn clean package sonar:sonar'
                      }
                    }
         }
    }
    post {
        always {
            echo 'This will always run'
        }
    }
}
