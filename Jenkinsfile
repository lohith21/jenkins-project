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
                withCredentials([usernamePassword(credentialsId: 'AnsiJenkins', usernameVariable: 'vagrant_user', passwordVariable: 'vagrant_password')]){
				sh '''
				   echo ${vagrant_user}
				   echo ${vagrant_password}
				   '''
                }
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