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

        stage('lint and format') {
            parallel{
                stage('linting'){
                    steps{
                        echo "Linting code in nested state"
                    }
                }
                stage('formating'){
                    steps{
                        echo "Formating code in nested state"
                    }
                }
            }
        }

        stage('Setup') {
            steps {
                withCredentials([usernamePassword(credentialsId: 'github', usernameVariable: 'vagrant_user', passwordVariable: 'vagrant_password')]){
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
                withCredentials([usernamePassword(credentialsId: 'AnsiJenkins', keyFileVariable: 'mypass' )]){
                   sh '''
                   ssh -i $mypass vagrant@172.31.0.101 "echo Hello"
                   '''
            }
        }
}
}