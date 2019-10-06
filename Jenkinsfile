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
        stage('Build') {
            steps {
                sh 'mvn -B -DskipTests clean package'
            }
        }
        stage('Test') {
            steps {
                sh 'mvn test'
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
                    bat 'sonar:sonar'
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
