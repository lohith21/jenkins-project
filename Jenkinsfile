pipeline {
    agent any
    options{skipDefaultCheckout()}

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
                echo "The database IP is: ${env.DB_HOST}"
            }
        }
        stage('Test') {
            steps {
                sh "pytest"
                sh "whoami"
                echo "User name is ${env.USERNAME} and passowrd is ${env.PASSWORD}"
            }
        }
}
}