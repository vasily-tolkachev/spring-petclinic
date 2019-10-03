pipeline {
    agent any
    stages {
        stage('Test') {
            steps {
                mail bcc: '',
                        body: 'Test jenkins email notification',
                        cc: '', from: '', replyTo: '',
                        subject: 'Test jenkins email notification',
                        to: 'vasilii_tolkachev@epam.com'
            }
        }
    }
    post {
        always {
            echo 'This will always run'
        }
    }
}
