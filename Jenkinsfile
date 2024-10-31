pipeline {
    agent any
    options{skipDefaultCheckout()}
    environment {
        DB_HOST = '171.32.0.100'
        USERNAME = 'rld2'
        PASSWORD = 'RLD@123'
    }

    stages {
        stage('Checkout') {
            steps {
                git url: 'https://github.com/kodekloudhub/jenkins-project.git', branch: 'main'
                sh "ls -ltr"
            }
        }
        stage('Setup') {
            steps {
                sh "pip install -r requirements.txt"
                echo "The database IP is: ${DB_HOST}"
            }
        }
        stage('Test') {
            steps {
                sh "pytest"
                sh "whoami"
                echo "User name is ${USERNAME} and passowrd is ${PASSWORD}"
            }
        }
}
}