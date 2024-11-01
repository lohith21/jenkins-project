pipeline {
    agent any
    options{skipDefaultCheckout()}
    environment {
        GIT_CREDS = credentials('github') 
    }

    stages {
        stage('Checkout') {
            steps {
                echo "my creds: ${GIT_CREDS}"
                echo "Username: ${"GIT_CREDS_USR"}"
                echo "Password: ${"GIT_CREDS_PWD"}"
                git url: 'https://github.com/kodekloudhub/jenkins-project.git', branch: 'main'
                sh "ls -ltr"
            }
        }
        stage('Setup') {
            steps {
                sh "pip install -r requirements.txt"
            }
        }
        stage('Test') {
            steps {
                sh "pytest"
                sh "whoami"
            }
        }
}
}