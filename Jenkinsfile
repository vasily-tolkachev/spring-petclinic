pipeline {
    agent any
    stages {
        stage('Test') {
            steps {
                emailext body: 'dsvdsvs', subject: 'Test ', to: 'vasilii_tolkachev@epam.com'
            }
        }
    }
    post {
        always {
            echo 'This will always run'
        }
    }
}
